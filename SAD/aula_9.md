# Decision Support Systems

## Lesson 9

### `LOAD_DIM_PROMOTION`

The `LOAD_DIM_PROMOTION` process demonstrates how to load data into a promotions dimension table (`T_DIM_PROMOTION`) by comparing source data from `T_CLEAN_PROMOTIONS`. It uses the SQL `MERGE` statement to handle both inserts and updates efficiently.

```sql
MERGE INTO T_DIM_PROMOTION TARGET USING(
  SELECT
    id,
    NAME,
    start_date,
    end_date,
    reduction,
    on_outdoor,
    on_tv
  FROM
    T_CLEAN_PROMOTIONS
) SOURCE ON (TARGET.promo_natural_Key = SOURCE.ID)
WHEN MATCHED THEN
UPDATE
SET
  TARGET.promo_name = SOURCE.name,
  TARGET.promo_start_date = SOURCE.start_date,
  TARGET.promo_end_date = SOURCE.end_date,
  TARGET.promo_red_price = SOURCE.reduction,
  TARGET.promo_board = SOURCE.on_outdoor,
  TARGET.promo_advertise = SOURCE.on_tv
  WHEN NOT MATCHED THEN
INSERT
  (
    TARGET.promo_key,
    TARGET.promo_natural_Key,
    TARGET.promo_name,
    TARGET.promo_start_date,
    TARGET.promo_end_date,
    TARGET.promo_red_price,
    TARGET.promo_board,
    TARGET.promo_advertise
  )
VALUES
  (
    seq_dim_promotion.NEXTVAL,
    SOURCE.id,
    SOURCE.name,
    SOURCE.start_date,
    SOURCE.end_date,
    SOURCE.reduction,
    SOURCE.on_outdoor,
    SOURCE.on_tv
  );
```

### `PRODUCT_CURSOR`

The `PRODUCT_CURSOR` process uses a cursor to handle Slowly Changing Dimensions (SCD) Type 2 for product data. This approach ensures that we can track changes over time in specific attributes of the product dimension.

```sql
FOR rec IN products_cursor
LOOP
  -- SEARCH THE PRODUCT IN THE DIMENSION BY SELECTING SCD2 ATTRIBUTES
  BEGIN
    SELECT
      product_key,
      NVL(product_size_package, -1),
      NVL(product_type_package, -1),
      product_diet_type,
      NVL(product_liquid_weight, -1) INTO v_product_key,
      v_size_package,
      v_type_package,
      v_diet_type,
      v_liquid_weight
    FROM
      T_DIM_PRODUCT
    WHERE
      product_natural_key = rec.id
      AND is_expired_version = 'NO';

-- IF A RECORD WAS FOUND, THEN THE SOURCE PRODUCT IS IN FACT A NEW VERSION:
-- DID ANY OF THE SCD2 ATTRIBUTES CHANGE?
IF (rec.pack_size != v_size_package)
OR (rec.pack_type != v_type_package)
OR (rec.diet_type != v_diet_type)
OR (rec.liq_weight != v_liquid_weight) THEN
UPDATE
  T_DIM_PRODUCT
SET
  IS_EXPIRED_VERSION = 'YES'
WHERE
  PRODUCT_KEY = v_product_key
INSERT INTO
  T_DIM_PRODUCT (
    PRODUCT_KEY,
    PRODUCT_NATURAL_KEY,
    PRODUCT_NAME,
    PRODUCT_BRAND,
    PRODUCT_CATEGORY,
    PRODUCT_SIZE_PACKAGE,
    PRODUCT_TYPE_PACKAGE,
    PRODUCT_DIET_TYPE,
    PRODUCT_LIQUID_WEIGHT,
    IS_EXPIRED_VERSION
  )
VALUES
  (
    seq_dim_product.NEXTVAL,
    rec.id,
    rec.name,
    rec.brand,
    rec.category_name,
    rec.pack_size,
    rec.pack_type,
    rec.diet_type,
    rec.liq_weight,
    'NO'
  );

v_new_products := v_new_products + 1;

END;
```
