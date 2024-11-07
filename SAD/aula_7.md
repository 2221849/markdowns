# Decision Support Systems

## Lesson 7

Let's initiate the transformation process and monitor the outcomes:

```sql
-- Run the main transformation process in PCK_TRANSFORM
BEGIN
    PCK_TRANSFORM.main(FALSE);
END;
/

-- Check the ETL log to observe the results
SELECT * FROM T_LOG_ETL;
```

Now, let's focus on the execution of the `pck_transform.SCREEN_PRODUCT_DIMENSIONS` screen, which is the only one currently implemented.

### `SCREEN_PRODUCT_DIMENSIONS`

This procedure aims to detect data quality issues in the dimensions of products recorded in the `t_data_products` table, following specific business rules. It logs any identified issues without discarding the problematic data.

The cursor, `products_with_problems`, selects rows from the `t_data_products` table where data quality issues are found according to these criteria:

- **Rule 1:** If the `width`, `height`, or `depth` fields are `NULL` and the `pack_type` requires dimensions (as indicated in the `t_lookup_pack_dimensions` table), the row is flagged as problematic.
- **Rule 2:** If any of the `width`, `height`, or `depth` fields are greater than or equal to zero, but the `pack_type` should not have dimensions (according to `t_lookup_pack_dimensions`), it is also marked as an issue.

The `t_lookup_pack_dimensions` table serves to determine whether a specific `pack_type` is expected to have dimensions, based on the `has_dimensions` flag.

### `SCREEN_PRODUCT_WEIGHT`

The `SCREEN_PRODUCT_WEIGHT` procedure is structured similarly, but it screens for issues in the `liq_weight` and `pack_type` fields.

**Here’s how it works**:

```sql
PROCEDURE screen_product_weight (
  p_iteration_key t_tel_iteration.iteration_key % TYPE,
  p_source_key t_tel_source.source_key % TYPE,
  p_screen_order t_tel_schedule.screen_order % TYPE
) IS

CURSOR products_with_problems IS
SELECT
  ROWID
FROM
  t_data_products
WHERE
  rejected_by_screen = '0'
  AND (
      liq_weight IS NULL
      AND pack_type IS NOT NULL
   )
   OR (
      liq_weight IS NOT NULL
      AND pack_type IS NULL
   );

i PLS_INTEGER := 0;

v_screen_name VARCHAR2(30) := 'screen_product_weight';

BEGIN
  pck_log.write_log(
    '  Starting SCREEN ["' || UPPER(v_screen_name) || '"] with order #' || p_screen_order || ''
  );

FOR rec IN products_with_problems
LOOP
  error_log(
    v_screen_name,
    SYSDATE,
    p_source_key,
    p_iteration_key,
    rec.rowid
  );

-- Reject the line with quality error.
UPDATE
   t_data_products
SET
   rejected_by_screen = '1' -- Only records not yet rejected
WHERE
   ROWID = rec.rowid;

i := i + 1;

END
LOOP
;

pck_log.write_log(
  '    Data quality problems in ' || i || ' row(s).',
  '    Done!'
);

EXCEPTION
  WHEN NO_DATA_FOUND THEN pck_log.write_log(
    '    No data quality problems found.',
    '    Done!'
  );

WHEN OTHERS THEN pck_log.write_uncomplete_task_msg;

RAISE e_transformation;

END;
```

**Screening Conditions**:

- **Condition 1**: If liq_weight is NULL while pack_type has a value, the row is flagged.

- **Condition 2**: If liq_weight has a value but pack_type is NULL, the row is also flagged.

### `SCREEN_PRODUCT_BRANDS`

The `SCREEN_PRODUCT_BRANDS` procedure screens for invalid product brands based on entries in the `t_lookup_brands` table. It flags rows with incorrect brand values, based on a predefined list of known incorrect brands.

```sql
PROCEDURE screen_product_brands (
  p_iteration_key t_tel_iteration.iteration_key % TYPE,
  p_source_key t_tel_source.source_key % TYPE,
  p_screen_order t_tel_schedule.screen_order % TYPE
) IS

CURSOR products_with_problems IS
SELECT
   ROWID
FROM
   t_data_products
WHERE
   rejected_by_screen = '0' -- Only records not yet rejected
   AND brand IN (
      SELECT
         brand_wrong
      FROM
         t_lookup_brands
   );
i PLS_INTEGER := 0;

v_screen_name VARCHAR2(30) := 'screen_product_brands';

BEGIN
  pck_log.write_log(
    '  Starting SCREEN ["' || UPPER(v_screen_name) || '"] with order #' || p_screen_order || ''
  );

FOR rec IN products_with_problems
LOOP
   error_log(
      v_screen_name,
      SYSDATE,
      p_source_key,
      p_iteration_key,
      rec.rowid
   );

i := i + 1;

END
LOOP
;

pck_log.write_log(
  '    Data quality problems in ' || i || ' row(s).',
  '    Done!'
);

EXCEPTION
  WHEN NO_DATA_FOUND THEN pck_log.write_log(
    '    No data quality problems found.',
    '    Done!'
  );

WHEN OTHERS THEN pck_log.write_uncomplete_task_msg;

RAISE e_transformation;

END;
```

**Screening Condition**:

- **Condition**: If the brand field in `t_data_products` contains a value found in the `brand_wrong` column of `t_lookup_brands`, the row is flagged as problematic.

### `TRANSFORM_PRODUCTS`

The `TRANSFORM_PRODUCTS` procedure corrects any detected errors in the `brand` column based on flagged entries and populates the `t_clean_products` table with transformed data.

```sql
-- Insert cleaned product data into t_clean_products
INSERT INTO
   t_clean_products(
      id,
      name,
      brand,
      pack_size,
      pack_type,
      diet_type,
      liq_weight,
      category_name
   )
SELECT
   prod.id,
   UPPER(prod.name) AS name,
   UPPER(prod.brand) AS brand,
   height || 'x' || width || 'x' || depth AS pack_size,
   UPPER(prod.pack_type) AS pack_type,
   cal.type AS diet_type,
   prod.liq_weight,
   UPPER(cat.name) AS category_name
FROM
   t_data_products prod
   JOIN t_data_categories cat ON prod.category_id = cat.id
   JOIN t_lookup_calories cal ON (
      prod.calories_100g BETWEEN cal.min_calories_100g
      AND cal.max_calories_100g
   )
WHERE
   prod.rejected_by_screen = '0'
   AND prod.calories_100g >= cal.min_calories_100g
   AND prod.calories_100g <= cal.max_calories_100g;

-- Update brands in t_clean_products where brand errors are detected
UPDATE
   t_clean_products clean
SET
   clean.brand = (
      SELECT
         UPPER(brand.brand_transformed)
      FROM
         t_lookup_brands brand
      WHERE
         UPPER(clean.brand) = UPPER(brand.brand_wrong)
   )
WHERE
   EXISTS (
      SELECT
         1
      FROM
         t_lookup_brands brand
      WHERE
         UPPER(clean.brand) = UPPER(brand.brand_wrong)
   );
```

### `TRANSFORM_PROMOTIONS`

The `TRANSFORM_PROMOTIONS` procedure normalizes data in the `t_clean_promotions` table and ensures promotions data aligns with the logical data map.

```sql
-- ******************************************************************
-- * TRANSFORMATION OF PROMOTIONS ACCORDING TO THE LOGICAL DATA MAP *
-- ******************************************************************

PROCEDURE transform_promotions IS
BEGIN
   pck_log.write_log('  Transforming data ["TRANSFORM_PROMOTIONS"]');

   -- Insert cleaned promotion data into t_clean_promotions
   INSERT INTO
      t_clean_promotions (
         id,
         name,
         start_date,
         end_date,
         reduction,
         on_outdoor,
         on_tv
      )
   SELECT
      p.id,
      UPPER(p.name) AS name,
      p.start_date,
      p.end_date,
      p.reduction,
      CASE
         WHEN p.on_outdoor = 1 THEN 'YES'
         ELSE 'NO'
      END AS on_outdoor,
      CASE
         WHEN p.on_tv = 1 THEN 'YES'
         ELSE 'NO'
      END AS on_tv
   FROM
      t_data_promotions p
   WHERE
      p.rejected_by_screen = '0';

   pck_log.write_log('    Done!');

EXCEPTION
   WHEN NO_DATA_FOUND THEN
      pck_log.write_log('    Found no lines to transform');
      pck_log.write_log('    Done!');
   WHEN OTHERS THEN
      pck_log.write_uncomplete_task_msg;
      RAISE e_transformation;

END;
```

### Calling the Procedures

Ensure that you call both `TRANSFORM_PRODUCTS` and `TRANSFORM_PROMOTIONS` procedures after defining them in the correct order, if necessary, to complete the transformation process.
