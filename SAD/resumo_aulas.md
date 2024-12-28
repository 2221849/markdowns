# **Decision Support Systems**

## **Source Views Utilized in the ETL Process**

```sql
-- Retrieve all source views from the external system
SELECT VIEW_NAME
FROM ALL_VIEWS@DBLINK_SADSB
WHERE OWNER = 'SB_READONLY';
```

## **ETL Pipeline Execution**

```sql
-- Execute the complete ETL pipeline: Extraction, Transformation, and Loading
EXEC PCK_EXTRACT.main(TRUE);
EXEC PCK_TRANSFORM.main(TRUE);
EXEC PCK_LOAD.main(TRUE, TRUE);

-- Verify the ETL execution status and check logs
SELECT LOG_TEXT FROM T_LOG_ETL;

-- Check the final extracted data in the fact table
SELECT * FROM T_FACT_LINEOFSALE;
```

## **Simplified Relevant Extraction Procedures**

### `initialize_extractions_table`

```sql
PROCEDURE initialize_extractions_table IS
BEGIN
   -- Remove any existing records from the extraction-related tables to reset them.
   DELETE FROM t_info_extractions;
   DELETE FROM t_data_stores_new;
   DELETE FROM t_data_stores_old;
   DELETE FROM t_data_managers_new;
   DELETE FROM t_data_managers_old;
   DELETE FROM t_data_celsius;

   -- Insert initial extraction information into the t_info_extractions table.
   INSERT INTO t_info_extractions (last_timestamp, source_table_name)
      VALUES (NULL, 'view_clientes@DBLINK_SADSB');
   INSERT INTO t_info_extractions (last_timestamp, source_table_name)
      VALUES (NULL, 'view_produtos@DBLINK_SADSB');
   INSERT INTO t_info_extractions (last_timestamp, source_table_name)
      VALUES (NULL, 'view_promocoes@DBLINK_SADSB');
   INSERT INTO t_info_extractions (last_timestamp, source_table_name)
      VALUES (NULL, 'view_linhasvenda_promocoes@DBLINK_SADSB');
   INSERT INTO t_info_extractions (last_timestamp, source_table_name)
      VALUES (NULL, 'view_linhasvenda@DBLINK_SADSB');
   INSERT INTO t_info_extractions (last_timestamp, source_table_name)
      VALUES (NULL, 'view_vendas@DBLINK_SADSB');
END;
```

### `table_extract`

```sql
PROCEDURE table_extract (
    p_source_table    VARCHAR2,
    p_attributes_src  VARCHAR2,
    p_attributes_dest VARCHAR2,
    p_dsa_table       VARCHAR2
) IS
    v_end_date        TIMESTAMP;
    v_start_date      t_info_extractions.LAST_TIMESTAMP%TYPE;
    v_sql             VARCHAR2(1000);
BEGIN
    -- Step 1: Clean Target Table (Delete Existing Data)
    v_sql := 'DELETE FROM ' || p_dsa_table;
    EXECUTE IMMEDIATE v_sql;

    -- Step 2: Get the Last Extraction Timestamp for the Given Source Table
    v_sql := 'SELECT last_timestamp
              FROM t_info_extractions
              WHERE UPPER(source_table_name) = ''' || UPPER(p_source_table) || '''';
    EXECUTE IMMEDIATE v_sql INTO v_start_date;

    -- If no previous extraction exists, use the oldest date for extraction
    IF v_start_date IS NULL THEN
        v_start_date := C_OLDEST_DATE;
    END IF;

    -- Step 3: Find the Record where the Extraction Must Stop
    v_sql := 'SELECT MAX(src_last_changed)
              FROM ' || p_source_table || '
              WHERE src_last_changed > :1';
    EXECUTE IMMEDIATE v_sql INTO v_end_date USING v_start_date;

    -- If no records were found to extract (v_end_date is NULL), exit the procedure
    IF v_end_date IS NOT NULL THEN
        -- Step 4: Extract Records from the Source Table to the Target Table
        v_sql := 'INSERT INTO ' || p_dsa_table || ' (' || p_attributes_dest || ')
                  SELECT ' || p_attributes_src || '
                  FROM ' || p_source_table || '
                  WHERE src_last_changed > :1
                  AND src_last_changed <= :2';
        EXECUTE IMMEDIATE v_sql USING v_start_date, v_end_date;

        -- Step 5: Update the Last Extraction Timestamp in `t_info_extractions`
        v_sql := 'UPDATE t_info_extractions
                  SET last_timestamp = :1
                  WHERE UPPER(source_table_name) = UPPER(''' || p_source_table || ''')';
        EXECUTE IMMEDIATE v_sql USING v_end_date;
    END IF;
END;
```

### `file_extract`

```sql
PROCEDURE file_extract (
    p_external_table   VARCHAR2,
    p_attributes_src   VARCHAR2,
    p_attributes_dest  VARCHAR2,
    p_dsa_table_new    VARCHAR2,
    p_dsa_table_old    VARCHAR2
) IS
    v_sql  VARCHAR2(1000);
BEGIN
    -- Step 1: Clean _old Target Table
    EXECUTE IMMEDIATE 'DELETE FROM ' || p_dsa_table_old;

    -- Step 2: Transfer the last extracted data to the _old Table
    v_sql := 'INSERT INTO ' || p_dsa_table_old || ' (' || p_attributes_dest || ') ' ||
    'SELECT ' || p_attributes_dest || ' FROM ' || p_dsa_table_new;
    EXECUTE IMMEDIATE v_sql;

    -- Step 3: Clean _new Table
    EXECUTE IMMEDIATE 'DELETE FROM ' || p_dsa_table_new;

    -- Step 4: Extract Data from Source File to _new Table
    EXECUTE IMMEDIATE 'INSERT INTO ' || p_dsa_table_new || ' (' || p_attributes_dest || ') ' ||
    'SELECT ' || p_attributes_src || ' FROM ' || p_external_table;
END;
```

### `table_extract_non_incremental`

```sql
PROCEDURE table_extract_non_incremental (
    p_source_table    VARCHAR2,
    p_DSA_table       VARCHAR2,
    p_attributes_src  VARCHAR2,
    p_attributes_dest VARCHAR2
) IS
    v_sql  VARCHAR2(1000);
BEGIN
    -- Step 1: Clean Target Table
    EXECUTE IMMEDIATE 'DELETE FROM ' || p_DSA_table;

    -- Step 2: Extract All Records from Source to Target Table
    -- setting 'rejected_by_screen' to '0' for all records.
    v_sql := 'INSERT INTO ' || p_DSA_table || ' (' || p_attributes_dest || ', rejected_by_screen) ' ||
    'SELECT ' || p_attributes_src || ', ''0'' FROM ' || p_source_table;
    EXECUTE IMMEDIATE v_sql;
END;

```

### `web_extract`

```sql
PROCEDURE web_extract (
    p_src_link          VARCHAR2,
    p_DSA_table         VARCHAR2,
    p_src_json_query    VARCHAR2,
    p_target_attributes VARCHAR2
) IS
    v_sql VARCHAR2(1000);
BEGIN
    -- Step 1: Clear temporary table for JSON data
    DELETE FROM t_data_JSON_temp;

    -- Step 2: Clear the target table
    EXECUTE IMMEDIATE 'DELETE FROM ' || p_DSA_table;

    -- Step 3: Insert JSON data into the temporary table
    INSERT INTO t_data_JSON_temp
    VALUES (pck_utilities.read_web_data(p_src_link));

    -- Step 4: Insert the extracted data into the target DSA table
    v_sql := 'INSERT INTO ' || p_DSA_table || ' (' || p_target_attributes || ') ' || p_src_json_query;
    EXECUTE IMMEDIATE v_sql;
END;
```

### `main`

```sql
PROCEDURE main (p_initialize BOOLEAN) IS
BEGIN
   -- Initialize the extraction table 't_info_extractions' if the flag is TRUE
   IF p_initialize = TRUE THEN
      initialize_extractions_table;
   END IF

   table_extract(
      'view_clientes@dblink_sadsb',
      'src_id,src_card_number,src_name,src_address,src_location,src_district,src_zip_code,src_phone_nr,src_gender,src_age,src_marital_status',
      'id,card_number,name,address,location,district,zip_code,phone_nr,gender,age,marital_status',
      't_data_customers'
   );

   table_extract(
      'view_produtos@dblink_sadsb',
      'src_id,src_name,src_brand,src_width,src_height,src_depth,src_pack_type,src_calories_100g,src_liq_weight,src_category_id',
      'id,name,brand,width,height,depth,pack_type,calories_100g,liq_weight,category_id',
      't_data_products'
   );

   table_extract(
      'view_promocoes@dblink_sadsb',
      'src_id,src_name,src_start_date,src_end_date,src_reduction,src_on_outdoor,src_on_tv',
      'id,name,start_date,end_date,reduction,on_outdoor,on_tv',
      't_data_promotions'
   );

   table_extract(
      'view_linhasvenda_promocoes@dblink_sadsb',
      'src_line_id,src_promo_id',
      'line_id,promo_id',
      't_data_linesofsalepromotions'
   );

   table_extract(
      'view_linhasvenda@dblink_sadsb',
      'src_id,src_sale_id,src_product_id,src_quantity,src_ammount_paid,src_line_date',
      'id,sale_id,product_id,quantity,ammount_paid,line_date',
      't_data_linesofsale'
   );

   table_extract(
      'view_vendas@dblink_sadsb',
      'src_id,src_store_id,src_customer_id',
      'id,store_id,customer_id',
      't_data_sales'
   );

   table_extract_non_incremental(
      'view_categorias@dblink_sadsb',
      't_data_categories',
      'src_id,src_name',
      'id,name'
   );

   table_extract_non_incremental(
      'view_registos@dblink_sadsb',
      't_data_customers_reg',
      'src_card_number, src_customer_type',
      'card_number, customer_type'
   );

   file_extract(
      't_ext_stores',
      'name,refer,building,address,zip_code,city,district,phone_nrs,fax_nr,closure_date',
      'name,reference,building,address,zip_code,location,district,telephones,fax,closure_date',
      't_data_stores_new',
      't_data_stores_old'
   );

   file_extract(
      't_ext_managers',
      'store_refer,name,hiring_date',
      'reference,manager_name,manager_since',
      't_data_managers_new',
      't_data_managers_old'
   );

   web_extract(
      'http://api.ipma.pt/open-data/forecast/meteorology/cities/daily/hp-daily-forecast-day0.json',
      't_data_celsius',
      'SELECT t.data_.forecastDate, jt.globalIdLocal, jt.tMin, jt.tMax FROM t_data_json_temp t, JSON_TABLE(t.data_, ''$.data[*]'' COLUMNS(globalIdLocal INTEGER PATH ''$.globalIdLocal'', tMin INTEGER PATH ''$.tMin'', tMax INTEGER PATH ''$.tMax'')) AS jt',
      'forecast_date,id_local,t_min,t_max'
   );
END;
```

## **Simplified Relevant Transformation Procedures**

### `screen_product_dimensions`

```sql
PROCEDURE screen_product_dimensions (
  p_iteration_key t_tel_iteration.iteration_key%TYPE,
  p_source_key t_tel_source.source_key%TYPE,
  p_screen_order t_tel_schedule.screen_order%TYPE
) IS
   -- Declare a cursor to search for extracted products with dimension-related issues
   CURSOR products_with_problems IS
      SELECT rowid
      FROM t_data_products
      WHERE rejected_by_screen = '0'
        AND (
            -- Condition for products with missing dimensions where the pack type expects dimensions
            ((width IS NULL OR height IS NULL OR depth IS NULL)
             AND UPPER(pack_type) IN (
                SELECT pack_type
                FROM t_lookup_pack_dimensions
                WHERE has_dimensions = '1'
             ))
            OR
            -- Condition for products with invalid dimensions where the pack type doesn't expect dimensions
            ((width >= 0 OR height >= 0 OR depth >= 0)
             AND UPPER(pack_type) IN (
                SELECT pack_type
                FROM t_lookup_pack_dimensions
                WHERE has_dimensions = '0'
             ))
        );

   -- Initialize local variables
   i PLS_INTEGER := 0;  -- Counter for processed records
   v_screen_name VARCHAR2(30) := 'screen_product_dimensions';  -- Name of the screen for error logging

BEGIN
   -- Loop through each product with detected dimension problems
   FOR rec IN products_with_problems LOOP
      -- Log the error details into the transformation error logger, but do not reject the line
      error_log(v_screen_name, SYSDATE, p_source_key, p_iteration_key, rec.rowid);

      -- Increment the counter for processed records
      i := i + 1;
   END LOOP;
END;
```

### `screen_product_brands`

```sql
PROCEDURE screen_product_brands (
  p_iteration_key t_tel_iteration.iteration_key%TYPE,
  p_source_key t_tel_source.source_key%TYPE,
  p_screen_order t_tel_schedule.screen_order%TYPE
) IS
   -- Declare a cursor to search for products that have incorrect brand information
   CURSOR products_with_problems IS
      SELECT p.rowid
      FROM t_data_products p
      JOIN t_lookup_brands b ON p.brand = b.brand_wrong
      WHERE p.rejected_by_screen = '0';

   -- Local variable to count the number of processed records
   i PLS_INTEGER := 0;

   -- Name of the screen for logging purposes
   v_screen_name VARCHAR2(30) := 'screen_product_brands';

BEGIN
   -- Loop through each product with an identified brand issue
   FOR rec IN products_with_problems LOOP
      -- Log the error details into the transformation error logger, without rejecting the line
      error_log(v_screen_name, SYSDATE, p_source_key, p_iteration_key, rec.rowid);

      -- Increment the counter for the processed records
      i := i + 1;
   END LOOP;
END;
```

### `screen_product_weight`

```sql
PROCEDURE screen_product_weight (
  p_iteration_key t_tel_iteration.iteration_key%TYPE,
  p_source_key t_tel_source.source_key%TYPE,
  p_screen_order t_tel_schedule.screen_order%TYPE
) IS
   -- Declare a cursor to search for products with weight-related issues
   CURSOR products_with_problems IS
      SELECT rowid
      FROM t_data_products
      WHERE rejected_by_screen = '0'
        AND (
            -- Condition for products where 'liq_weight' is missing but 'pack_type' is present
            (liq_weight IS NULL AND pack_type IS NOT NULL)
            OR
            -- Condition for products where 'pack_type' is missing but 'liq_weight' is present
            (liq_weight IS NOT NULL AND pack_type IS NULL)
        );

   -- Local variable to count the number of processed records
   i PLS_INTEGER := 0;

   -- Name of the screen for error logging purposes
   v_screen_name VARCHAR2(30) := 'screen_product_weight';

BEGIN
   -- Loop through each product with identified weight-related problems
   FOR rec IN products_with_problems LOOP
      -- Log the error details into the transformation error logger
      error_log(v_screen_name, SYSDATE, p_source_key, p_iteration_key, rec.rowid);

      -- Mark the product as rejected by setting 'rejected_by_screen' to '1'
      UPDATE t_data_products
      SET rejected_by_screen = '1'
      WHERE rowid = rec.rowid;

      -- Increment the counter for processed records
      i := i + 1;
   END LOOP;
END;
```

### `transform_customers`

```sql
PROCEDURE transform_customers IS
BEGIN
   -- Insert customer data into the clean customer table 't_clean_customers'
   -- The data is transformed according to logical data map
   INSERT INTO t_clean_customers (
      id,
      card_number,
      name,
      customer_type,
      address,
      location,
      district,
      zip_code,
      phone_nr,
      gender,
      age,
      marital_status
   )
   SELECT
      id,
      r.card_number,
      UPPER(name),  -- Convert name to uppercase
      UPPER(r.customer_type),  -- Convert customer type to uppercase
      UPPER(address),  -- Convert address to uppercase
      UPPER(location),  -- Convert location to uppercase
      UPPER(district),  -- Convert district to uppercase
      zip_code,
      phone_nr,

      -- Transform 'gender' field to a standardized value
      CASE UPPER(gender)
         WHEN 'M' THEN 'MALE'
         WHEN 'F' THEN 'FEMALE'
         ELSE 'OTHER'
      END,

      age,

      -- Transform 'marital_status' field to a standardized value
      CASE UPPER(marital_status)
         WHEN 'C' THEN 'MARRIED'
         WHEN 'S' THEN 'SINGLE'
         WHEN 'V' THEN 'WIDOW'
         WHEN 'D' THEN 'DIVORCED'
         ELSE 'OTHER'
      END
   FROM
      t_data_customers c
   JOIN
      t_data_customers_reg r ON c.card_number = r.card_number
   WHERE
      c.rejected_by_screen = '0';  -- Only include records that have not been rejected by the screen

END;

```

### `transform_products`

```sql
PROCEDURE transform_products IS
BEGIN
   -- Insert transformed product data into 't_clean_products'
   -- The data is transformed according to logical data map
   INSERT INTO t_clean_products (
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
      p.id,
      UPPER(p.name),  -- Convert product name to uppercase
      UPPER(p.brand),  -- Convert brand to uppercase
      height || 'x' || width || 'x' || depth,  -- Concatenate pack dimensions (height x width x depth)
      UPPER(p.pack_type),  -- Convert pack type to uppercase
      UPPER(l.type),  -- Convert diet type to uppercase based on calories
      p.liq_weight,
      UPPER(c.name)  -- Convert category name to uppercase
   FROM
      t_data_products p
   JOIN
      t_lookup_calories l
      ON p.calories_100g BETWEEN l.min_calories_100g AND l.max_calories_100g  -- Match calories range
   JOIN
      t_data_categories c
      ON c.id = p.category_id  -- Join category table on category ID
   WHERE
      c.rejected_by_screen = '0'  -- Only include categories that are not rejected
      AND p.rejected_by_screen = '0';  -- Only include products that are not rejected

   -- Update the 'brand' field in the 't_clean_products' table by transforming brands
   -- based on the 'brand_wrong' in the 't_lookup_brands' table
   UPDATE t_clean_products p
   SET brand = (
      SELECT brand_transformed
      FROM t_lookup_brands b
      WHERE p.brand = b.brand_wrong  -- Match brands that need transformation
   )
   WHERE
      p.brand IN (SELECT brand_wrong FROM t_lookup_brands);  -- Only update products with 'wrong' brand
END;
```

### `transform_promotions`

```sql
PROCEDURE transform_promotions IS
BEGIN
   -- Insert transformed promotion data into 't_clean_promotions'
   -- The data is transformed according to logical data map
   INSERT INTO t_clean_promotions (
      id,
      name,
      start_date,
      end_date,
      reduction,
      on_outdoor,
      on_tv
   )
   SELECT
      id,
      UPPER(name),  -- Convert promotion name to uppercase
      start_date,
      end_date,
      reduction,

      -- Convert 'on_outdoor' from numeric (1) to 'YES' and (0) to 'NO'
      CASE on_outdoor
         WHEN 1 THEN 'YES'
         ELSE 'NO'
      END,

      -- Convert 'on_tv' from numeric (1) to 'YES' and (0) to 'NO'
      CASE on_tv
         WHEN 1 THEN 'YES'
         ELSE 'NO'
      END
   FROM
      t_data_promotions
   WHERE
      rejected_by_screen = '0';  -- Only include records that are not rejected by the screen
END;
```

### `transform_linesofsale`

```sql
PROCEDURE transform_linesofsale IS
BEGIN
   -- Insert transformed sales line data into 't_clean_linesofsale'
   -- The data is transformed according to logical data map
   INSERT INTO t_clean_linesofsale (
      id,
      sale_id,
      product_id,
      quantity,
      ammount_paid,
      line_date,
      promo_id,
      store_id,
      customer_id
   )
   SELECT
      l.id,
      l.sale_id,
      l.product_id,
      l.quantity,
      l.ammount_paid,
      l.line_date,
      p.promo_id,  -- Join with promotions if available
      s.store_id,  -- Join with store information
      s.customer_id  -- Join with customer information
   FROM
      t_data_linesofsale l
   JOIN
      t_data_sales s
      ON l.sale_id = s.id  -- Join lines of sale with sales information
   LEFT JOIN
      t_data_linesofsalepromotions p
      ON (l.id = p.line_id AND p.rejected_by_screen = '0')  -- Left join with promotions to get promo_id, if applicable
   WHERE
      l.rejected_by_screen = '0'  -- Only include lines that are not rejected
      AND s.rejected_by_screen = '0';  -- Only include sales records that are not rejected
END;
```

### `transform_stores`

```sql
PROCEDURE transform_stores IS
BEGIN
   -- Insert transformed store data into 't_clean_stores'
   -- The data is transformed according to logical data map
   INSERT INTO t_clean_stores (
      name,
      reference,
      address,
      zip_code,
      location,
      district,
      telephones,
      fax,
      status,
      manager_name,
      manager_since
   )
   SELECT
      UPPER(name),  -- Convert store name to uppercase
      UPPER(s.reference),  -- Convert store reference to uppercase
      -- Concatenate building (if available), address, zip code, and location into a single address field
      UPPER(CASE building
         WHEN '-' THEN NULL
         ELSE building || ' - '
      END || address || ' / ' || zip_code || ', ' || location),
      zip_code,  -- Zip code
      UPPER(location),  -- Convert location to uppercase
      UPPER(district),  -- Convert district to uppercase
      -- Format phone numbers by removing dots and spaces, then taking the first 9 characters
      SUBSTR(REPLACE(REPLACE(telephones, '.', ''), ' ', ''), 1, 9),
      fax,  -- Fax number
      -- Set store status based on closure date: 'ACTIVE' if closure_date is NULL, 'INACTIVE' otherwise
      CASE
         WHEN closure_date IS NULL THEN 'ACTIVE'
         ELSE 'INACTIVE'
      END,
      UPPER(manager_name),  -- Convert manager name to uppercase
      manager_since  -- Manager's tenure (since)
   FROM
      -- Select stores from 't_data_stores_new' that are not present in 't_data_stores_old'
      (
         SELECT name, reference, building, address, zip_code, location, district, telephones, fax, closure_date
         FROM t_data_stores_new
         WHERE rejected_by_screen = '0'
         MINUS
         SELECT name, reference, building, address, zip_code, location, district, telephones, fax, closure_date
         FROM t_data_stores_old
      ) s
   JOIN
      t_data_managers_new d
      ON s.reference = d.reference  -- Join with 't_data_managers_new' to get manager information
   WHERE
      d.rejected_by_screen = '0';  -- Only include stores with managers that are not rejected
END;
```

### `transform_celsius`

```sql
PROCEDURE transform_celsius IS
BEGIN
   -- Insert transformed weather data into 't_clean_celsius'
   -- The data is transformed according to logical data map
   INSERT INTO t_clean_celsius (
      forecast_date,
      temperature_status
   )
   SELECT
      -- Convert forecast date to 'dd/mm/yyyy' format
      TO_CHAR(TO_DATE(forecast_date, 'yyyy-mm-dd'), 'dd/mm/yyyy'),

      -- Classify temperature based on average forecast value
      CASE
         WHEN forecast_value < 4 THEN 'COLD'  -- Below 4°C: classified as 'COLD'
         WHEN forecast_value < 10 THEN 'FRESH'  -- Between 4°C and 10°C: classified as 'FRESH'
         WHEN forecast_value < 25 THEN 'NICE'  -- Between 10°C and 25°C: classified as 'NICE'
         ELSE 'HOT'  -- Above 25°C: classified as 'HOT'
      END
   FROM
      (
         -- Subquery to calculate average temperature based on max and min temperatures for each forecast date
         SELECT forecast_date,
                AVG((t_max + t_min) / 2) AS forecast_value  -- Calculate average of max and min temperature
         FROM t_data_celsius
         GROUP BY forecast_date  -- Group by forecast date to get daily averages
      );
END;
```

### `main`

```sql
PROCEDURE main (p_duplicate_last_iteration BOOLEAN) IS
    -- Cursor to retrieve all scheduled screens for the given iteration
    CURSOR scheduled_screens_cursor(p_iteration_key t_tel_iteration.iteration_key%TYPE) IS
        SELECT UPPER(screen_name) AS screen_name,
               source_key,
               screen_order
        FROM t_tel_schedule
        JOIN t_tel_screen
            ON t_tel_schedule.screen_key = t_tel_screen.screen_key
        WHERE iteration_key = p_iteration_key
        ORDER BY screen_order ASC;

    -- Variable to store the iteration key
    v_iteration_key t_tel_iteration.iteration_key%TYPE;
    v_sql VARCHAR2(200);

BEGIN
    -- Clean up the temporary tables before processing
    DELETE FROM t_clean_customers;
    DELETE FROM t_clean_products;
    DELETE FROM t_clean_promotions;
    DELETE FROM t_clean_linesofsale;
    DELETE FROM t_clean_stores;
    DELETE FROM t_clean_celsius;

    -- Retrieve the most recent iteration key
    BEGIN
        SELECT MAX(iteration_key)
        INTO v_iteration_key
        FROM t_tel_iteration;
    END;

    -- If flag is set to duplicate last iteration, do so
    IF p_duplicate_last_iteration THEN
        v_iteration_key := duplicate_iteration(v_iteration_key);
    END IF;

    -- Start the iteration by setting the start date
    UPDATE t_tel_iteration
    SET iteration_start_date = systimestamp
    WHERE iteration_key = v_iteration_key;

    -- Execute dynamic SQL for each screen in the scheduled screens cursor
    FOR rec IN scheduled_screens_cursor(v_iteration_key) LOOP
        v_sql := 'BEGIN pck_transform.' || rec.screen_name ||
                 '(' || v_iteration_key || ',' || rec.source_key || ',' || rec.screen_order || '); END;';
        EXECUTE IMMEDIATE v_sql;
    END LOOP;

    -- End the iteration by setting the end date and calculating the duration
    UPDATE t_tel_iteration
    SET iteration_end_date = systimestamp,
        iteration_duration_real = EXTRACT(SECOND FROM (systimestamp - iteration_start_date))
    WHERE iteration_key = v_iteration_key;

    -- Call transformation procedures for various data entities
    transform_customers;
    transform_products;
    transform_promotions;
    transform_linesofsale;
    transform_stores;
    transform_celsius;

    COMMIT;
END;
```

### `PCK_TRANSFORM`

```sql
CREATE OR REPLACE PACKAGE PCK_TRANSFORM AS

   -- Main procedure to orchestrate the transformation process
   PROCEDURE main (p_duplicate_last_iteration BOOLEAN);

   -- Procedure to handle product dimensions screen transformation
   PROCEDURE screen_product_dimensions (
       p_iteration_key t_tel_iteration.iteration_key%TYPE,
       p_source_key t_tel_source.source_key%TYPE,
       p_screen_order t_tel_schedule.screen_order%TYPE
   );

   -- Procedure to handle product brands screen transformation
   PROCEDURE screen_product_brands (
       p_iteration_key t_tel_iteration.iteration_key%TYPE,
       p_source_key t_tel_source.source_key%TYPE,
       p_screen_order t_tel_schedule.screen_order%TYPE
   );

   -- Procedure to handle product weight screen transformation
   PROCEDURE screen_product_weight (
       p_iteration_key t_tel_iteration.iteration_key%TYPE,
       p_source_key t_tel_source.source_key%TYPE,
       p_screen_order t_tel_schedule.screen_order%TYPE
   );

END PCK_TRANSFORM;
```

## **Simplified Relevant Load Procedures**

### `init_dimensions`

```sql
PROCEDURE init_dimensions IS
BEGIN

   -- Insert 'INVALID PRODUCT' into the product dimension
   INSERT INTO t_dim_product (
      product_key,
      product_natural_key,
      product_name,
      product_brand,
      product_category,
      product_size_package,
      product_type_package,
      product_diet_type,
      product_liquid_weight,
      is_expired_version
   ) VALUES (
      pck_error_codes.c_load_invalid_dim_record_key,
      pck_error_codes.c_load_invalid_dim_record_Nkey,
      'INVALID PRODUCT',
      NULL, NULL, NULL, NULL, NULL, NULL, 'NO'
   );

   -- Insert 'INVALID PROMOTION' into the promotion dimension
   INSERT INTO t_dim_promotion (
      promo_key,
      promo_natural_key,
      promo_name,
      promo_red_price,
      promo_advertise,
      promo_board,
      promo_start_date,
      promo_end_date
   ) VALUES (
      pck_error_codes.c_load_invalid_dim_record_key,
      pck_error_codes.c_load_invalid_dim_record_Nkey,
      'INVALID PROMOTION',
      NULL, NULL, NULL, NULL, NULL
   );

   -- Insert 'INVALID DATE' into the date dimension
   INSERT INTO t_dim_date (
      date_key,
      date_full_date,
      date_month_full,
      date_month_name,
      date_month_short_name,
      date_month_nr,
      date_quarter_nr,
      date_quarter_full,
      date_semester_nr,
      date_semester_full,
      date_event,
      date_year,
      date_day_nr,
      date_is_holiday
   ) VALUES (
      pck_error_codes.c_load_invalid_dim_record_key,
      'INVALID',
      NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL
   );

   -- Insert 'INVALID TIME' into the time dimension
   INSERT INTO t_dim_time (
      time_key,
      time_full_time,
      time_period_of_day,
      time_minutes_after_midnight,
      time_hour_nr,
      time_minute_nr,
      time_second_nr
   ) VALUES (
      pck_error_codes.c_load_invalid_dim_record_key,
      'INVALID',
      NULL, NULL, NULL, NULL, NULL
   );

   -- Insert 'INVALID STORE' into the store dimension
   INSERT INTO t_dim_store (
      store_key,
      store_natural_key,
      store_name,
      store_full_address,
      store_location,
      store_district,
      store_zip_code,
      store_main_phone,
      store_main_phone_old,
      store_fax,
      store_fax_old,
      store_manager_name,
      store_manager_since,
      store_state,
      is_expired_version
   ) VALUES (
      pck_error_codes.c_load_invalid_dim_record_key,
      pck_error_codes.c_load_invalid_dim_record_Nkey,
      'INVALID STORE',
      'NOT APPLICABLE',
      NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 'NO'
   );

   -- Insert 'INVALID CUSTOMER' into the customer dimension
   INSERT INTO t_dim_customer (
      customer_key,
      customer_natural_key,
      customer_card_number,
      customer_name,
      customer_address,
      customer_location,
      customer_district,
      customer_zip_code,
      customer_phone_nr,
      customer_gender,
      customer_gender_old,
      customer_age,
      customer_marital_status,
      is_expired_version
   ) VALUES (
      pck_error_codes.c_load_invalid_dim_record_key,
      pck_error_codes.c_load_invalid_dim_record_Nkey,
      NULL,
      'INVALID CUSTOMER',
      NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, NULL, 'NO'
   );

END;
```

### `load_dim_promotion`

```sql
PROCEDURE load_dim_promotion IS
BEGIN
   -- Merge promotions from the source table into the promotion dimension table.
   -- Handle new, updated, and unchanged records.

   MERGE INTO t_dim_promotion dim
   USING (
      SELECT
         id,
         name,
         start_date,
         end_date,
         reduction,
         on_outdoor,
         on_tv
      FROM t_clean_promotions
   ) clean
   ON (dim.promo_natural_key = clean.id)

   -- Update existing records if a match is found
   WHEN MATCHED THEN
      UPDATE SET
         dim.promo_name = clean.name,
         dim.promo_red_price = clean.reduction,
         dim.promo_advertise = clean.on_tv,
         dim.promo_board = clean.on_outdoor,
         dim.promo_start_date = clean.start_date,
         dim.promo_end_date = clean.end_date

   -- Insert new records if no match is found
   WHEN NOT MATCHED THEN
      INSERT (
         dim.promo_key,
         dim.promo_natural_key,
         dim.promo_name,
         dim.promo_red_price,
         dim.promo_advertise,
         dim.promo_board,
         dim.promo_start_date,
         dim.promo_end_date
      ) VALUES (
         seq_dim_promotion.NEXTVAL,
         clean.id,
         clean.name,
         clean.reduction,
         clean.on_tv,
         clean.on_outdoor,
         clean.start_date,
         clean.end_date
      );

END;
```

### `load_dim_product`

```sql
PROCEDURE load_dim_product IS
   -- Cursor to fetch cleaned product data
   CURSOR products_cursor IS
      SELECT id, name, brand, pack_size, pack_type, diet_type, liq_weight, category_name
      FROM t_clean_products;

   -- Statistic counters
   i INTEGER := 0;
   v_new_products INTEGER := 0;
   v_new_versions INTEGER := 0;
   v_old_versions INTEGER := 0;

   -- Variables for SCD checking
   v_product_key t_dim_product.product_key%TYPE;
   v_size_package t_dim_product.product_size_package%TYPE;
   v_type_package t_dim_product.product_type_package%TYPE;
   v_diet_type t_dim_product.product_diet_type%TYPE;
   v_liquid_weight t_dim_product.product_liquid_weight%TYPE;

BEGIN
   -- Loop through each record in the cleaned product data
   FOR rec IN products_cursor LOOP
      BEGIN
         -- Search for the product in the dimension table with active (non-expired) version
         SELECT product_key,
                NVL(product_size_package, -1),
                NVL(product_type_package, -1),
                product_diet_type,
                NVL(product_liquid_weight, -1)
         INTO v_product_key, v_size_package, v_type_package, v_diet_type, v_liquid_weight
         FROM t_dim_product
         WHERE product_natural_key = rec.id AND is_expired_version = 'NO';

         -- Check if any SCD2 attributes have changed
         IF NVL(rec.pack_size, -1) != v_size_package OR
            NVL(rec.pack_type, -1) != v_type_package OR
            rec.diet_type != v_diet_type OR
            rec.liq_weight != v_liquid_weight THEN

            -- Mark the existing version as expired
            UPDATE t_dim_product
            SET is_expired_version = 'YES'
            WHERE product_key = v_product_key;

            -- Insert the new version of the product
            INSERT INTO t_dim_product (
               product_key,
               product_natural_key,
               product_name,
               product_brand,
               product_category,
               product_size_package,
               product_type_package,
               product_diet_type,
               product_liquid_weight,
               is_expired_version
            )
            VALUES (
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

            -- Increment new versions counter
            v_new_versions := v_new_versions + 1;

         ELSE
            -- If no SCD2 attributes changed, update SCD1 attributes
            UPDATE t_dim_product
            SET product_name = rec.name,
                product_brand = rec.brand,
                product_category = rec.category_name
            WHERE product_key = v_product_key;

            -- Increment old versions counter
            v_old_versions := v_old_versions + 1;
         END IF;

      EXCEPTION
         WHEN NO_DATA_FOUND THEN
            -- If no active version exists, insert as a new product
            INSERT INTO t_dim_product (
               product_key,
               product_natural_key,
               product_name,
               product_brand,
               product_category,
               product_size_package,
               product_type_package,
               product_diet_type,
               product_liquid_weight,
               is_expired_version
            )
            VALUES (
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

            -- Increment new products counter
            v_new_products := v_new_products + 1;
      END;
   END LOOP;
END;
```

### `load_dim_customer`

```sql
PROCEDURE load_dim_customer IS
   -- Cursor to fetch cleaned customer data
   CURSOR customers_cursor IS
      SELECT id, card_number, name, address, location, district, zip_code, phone_nr, gender, age, marital_status, customer_type
      FROM t_clean_customers;

   -- Statistic counters
   i INTEGER := 0;
   v_new_customers INTEGER := 0;
   v_new_versions INTEGER := 0;
   v_old_versions INTEGER := 0;

   -- Variables for SCD checking
   v_key t_dim_customer.customer_key%TYPE;
   v_location t_dim_customer.customer_location%TYPE;
   v_district t_dim_customer.customer_district%TYPE;
   v_zip_code t_dim_customer.customer_zip_code%TYPE;
   v_gender t_dim_customer.customer_gender%TYPE;
   v_gender_old t_dim_customer.customer_gender%TYPE;
   v_age t_dim_customer.customer_age%TYPE;
   v_marital_status t_dim_customer.customer_marital_status%TYPE;
   v_customer_type t_dim_customer.customer_type%TYPE;

BEGIN
   -- Loop through each record in the cleaned customer data
   FOR rec IN customers_cursor LOOP
      BEGIN
         -- Search for the customer in the dimension table with active (non-expired) version
         SELECT customer_key,
                customer_location,
                customer_district,
                customer_zip_code,
                customer_gender,
                customer_age,
                customer_marital_status,
                customer_type
         INTO v_key, v_location, v_district, v_zip_code, v_gender, v_age, v_marital_status, v_customer_type
         FROM t_dim_customer
         WHERE customer_natural_key = rec.id AND is_expired_version = 'NO';

         -- Check if the SCD3 attribute (customer_gender) has changed
         v_gender_old := NULL;
         IF rec.gender <> v_gender THEN
            -- Store the old gender value
            v_gender_old := v_gender;
         END IF;

         -- Check if any SCD2 attributes have changed
         IF rec.location != v_location OR
            rec.district != v_district OR
            rec.zip_code != v_zip_code OR
            rec.customer_type != v_customer_type OR
            rec.age != v_age OR
            rec.marital_status != v_marital_status THEN

            -- Mark the existing version as expired
            UPDATE t_dim_customer
            SET is_expired_version = 'YES'
            WHERE customer_key = v_key;

            -- Insert the new version of the customer
            INSERT INTO t_dim_customer (
               customer_key,
               customer_natural_key,
               customer_card_number,
               customer_name,
               customer_address,
               customer_location,
               customer_district,
               customer_zip_code,
               customer_phone_nr,
               customer_gender,
               customer_gender_old,
               customer_age,
               customer_marital_status,
               customer_type,
               is_expired_version
            )
            VALUES (
               seq_dim_customer.NEXTVAL,
               rec.id,
               rec.card_number,
               rec.name,
               rec.address,
               rec.location,
               rec.district,
               rec.zip_code,
               rec.phone_nr,
               rec.gender,
               v_gender_old,
               rec.age,
               rec.marital_status,
               rec.customer_type,
               'NO'
            );

            -- Increment new versions counter
            v_new_versions := v_new_versions + 1;

         ELSE
            -- If no SCD2 attributes changed, update SCD1 and SCD3 attributes
            UPDATE t_dim_customer
            SET customer_card_number = rec.card_number,  -- SCD1
                customer_name = rec.name,                -- SCD1
                customer_address = rec.address,          -- SCD1
                customer_phone_nr = rec.phone_nr,        -- SCD1
                customer_gender = rec.gender,            -- SCD3
                customer_gender_old = v_gender_old       -- SCD3
            WHERE customer_key = v_key;

            -- Increment old versions counter
            v_old_versions := v_old_versions + 1;
         END IF;

      EXCEPTION
         WHEN NO_DATA_FOUND THEN
            -- If no active version exists, insert as a new customer
            INSERT INTO t_dim_customer (
               customer_key,
               customer_natural_key,
               customer_card_number,
               customer_name,
               customer_address,
               customer_location,
               customer_district,
               customer_zip_code,
               customer_phone_nr,
               customer_gender,
               customer_gender_old,
               customer_age,
               customer_marital_status,
               customer_type,
               is_expired_version
            )
            VALUES (
               seq_dim_customer.NEXTVAL,
               rec.id,
               rec.card_number,
               rec.name,
               rec.address,
               rec.location,
               rec.district,
               rec.zip_code,
               rec.phone_nr,
               rec.gender,
               NULL,
               rec.age,
               rec.marital_status,
               rec.customer_type,
               'NO'
            );

            -- Increment new customers counter
            v_new_customers := v_new_customers + 1;
      END;
   END LOOP;
END;
```

### `load_dim_store`

```sql
PROCEDURE load_dim_store IS
   -- Cursor to fetch cleaned store data
   CURSOR stores_cursor IS
      SELECT name, reference, address, zip_code, location, district, telephones, fax, status, manager_name, manager_since
      FROM t_clean_stores;

   -- Statistic counters
   i INTEGER := 0;
   v_new_stores INTEGER := 0;
   v_new_versions INTEGER := 0;
   v_old_versions INTEGER := 0;

   -- Variables for SCD checking
   v_store_key t_dim_store.store_key%TYPE;
   v_store_name t_dim_store.store_name%TYPE;
   v_manager_name t_dim_store.store_manager_name%TYPE;
   v_manager_since t_dim_store.store_manager_since%TYPE;
   v_store_main_phone t_dim_store.store_main_phone%TYPE;
   v_store_fax t_dim_store.store_fax%TYPE;
   v_old_main_phone t_dim_store.store_main_phone%TYPE;
   v_old_fax t_dim_store.store_fax%TYPE;

BEGIN
   -- Loop through each record in the cleaned store data
   FOR rec IN stores_cursor LOOP
      BEGIN
         -- Search for the store in the dimension table with active (non-expired) version
         SELECT store_key, store_name, store_manager_name, store_manager_since, store_main_phone, store_fax
         INTO v_store_key, v_store_name, v_manager_name, v_manager_since, v_store_main_phone, v_store_fax
         FROM t_dim_store
         WHERE store_natural_key = rec.reference AND is_expired_version = 'NO';

         -- Check if any of the SCD3 attributes (store_main_phone, store_fax) have changed
         v_old_main_phone := NULL;
         IF rec.telephones <> v_store_main_phone THEN
            -- Store the old phone value
            v_old_main_phone := v_store_main_phone;
         END IF;

         v_old_fax := NULL;
         IF rec.fax <> v_store_fax THEN
            -- Store the old fax value
            v_old_fax := v_store_fax;
         END IF;

         -- Check if any of the SCD2 attributes have changed
         IF rec.name != v_store_name OR
            rec.manager_name != v_manager_name OR
            rec.manager_since != v_manager_since THEN

            -- 1. Mark the existing version as expired
            UPDATE t_dim_store
            SET is_expired_version = 'YES'
            WHERE store_key = v_store_key;

            -- 2. Insert the new version of the store
            INSERT INTO t_dim_store (
               store_key, store_natural_key, store_name, store_full_address, store_location,
               store_district, store_zip_code, store_main_phone, store_main_phone_old, store_fax,
               store_fax_old, store_manager_name, store_manager_since, store_state, is_expired_version
            )
            VALUES (
               seq_dim_store.NEXTVAL, rec.reference, rec.name, rec.address, rec.location,
               rec.district, rec.zip_code, rec.telephones, v_old_main_phone, rec.fax,
               v_old_fax, rec.manager_name, rec.manager_since, rec.status, 'NO'
            );

            -- Increment new versions counter
            v_new_versions := v_new_versions + 1;

         ELSE
            -- If no SCD2 attributes changed, update SCD1 and SCD3 attributes
            UPDATE t_dim_store
            SET store_full_address = rec.address,         -- SCD1
                store_location = rec.location,            -- SCD1
                store_district = rec.district,            -- SCD1
                store_zip_code = rec.zip_code,            -- SCD1
                store_manager_since = rec.manager_since,  -- SCD1
                store_manager_name = rec.manager_name,    -- SCD1
                -- SCD3 attributes
                store_main_phone = rec.telephones,
                store_fax = rec.fax,
                store_main_phone_old = v_old_main_phone,
                store_fax_old = v_old_fax
            WHERE store_key = v_store_key;

            -- Increment old versions counter
            v_old_versions := v_old_versions + 1;
         END IF;

      EXCEPTION
         WHEN NO_DATA_FOUND THEN
            -- If no active version exists, insert as a new store
            -- SCD3 _old attributes are not filled
            INSERT INTO t_dim_store (
               store_key, store_natural_key, store_name, store_full_address, store_location,
               store_district, store_zip_code, store_main_phone, store_main_phone_old, store_fax,
               store_fax_old, store_manager_name, store_manager_since, store_state, is_expired_version
            )
            VALUES (
               seq_dim_store.NEXTVAL, rec.reference, rec.name, rec.address, rec.location,
               rec.district, rec.zip_code, rec.telephones, NULL, rec.fax, NULL,
               rec.manager_name, rec.manager_since, rec.status, 'NO'
            );

            -- Increment new stores counter
            v_new_stores := v_new_stores + 1;
      END;
   END LOOP;
END;
```

### `load_dim_date`

```sql
PROCEDURE load_dim_date(p_load_dates_from_file BOOLEAN) IS
   -- Variable to hold today's date (if required for future logic)
   l_today VARCHAR2(10);
BEGIN
   -- Step 1: Load all date records from the external table `t_ext_dates` if the parameter `p_load_dates_from_file` is TRUE
   IF p_load_dates_from_file = TRUE THEN
      INSERT INTO t_dim_date (
         date_key,
         date_full_date,
         date_month_full,
         date_month_name,
         date_month_short_name,
         date_month_nr,
         date_quarter_nr,
         date_quarter_full,
         date_semester_nr,
         date_semester_full,
         date_day_nr,
         date_is_holiday,
         date_event,
         date_year
      )
      SELECT
         date_key,
         date_full_date,
         date_month_full,
         date_month_name,
         date_month_short_name,
         date_month_nr,
         date_quarter_nr,
         date_quarter_full,
         date_semester_nr,
         date_semester_full,
         date_day_nr,
         date_is_holiday,
         date_event,
         date_year
      FROM t_ext_dates;
   END IF;

   -- Step 2: Update the temperature status in `t_dim_date` based on data from `t_clean_celsius`
   UPDATE t_dim_date
   SET date_temperature_status = (
      SELECT temperature_status
      FROM t_clean_celsius
   )
   WHERE date_full_date = (
      SELECT forecast_date
      FROM t_clean_celsius
   );
END;
```

### `load_dim_time`

```sql
PROCEDURE load_dim_time IS
BEGIN
   INSERT INTO /*+ APPEND */ t_dim_time (
      time_key,
      time_full_time,
      time_period_of_day,
      time_minutes_after_midnight,
      time_hour_nr,
      time_minute_nr,
      time_second_nr
   )
   SELECT
      time_key,
      time_full_time,
      time_period_of_day,
      time_minutes_after_00,
      time_hour_nr,
      time_minute_nr,
      time_second_nr
   FROM t_ext_time;
END;

```

### `load_fact_table`

```sql
PROCEDURE load_fact_table IS
BEGIN
   -- Insert data into the fact table `t_fact_lineofsale`
   INSERT INTO t_fact_lineofsale (
      product_key,
      store_key,
      promo_key,
      date_key,
      time_key,
      customer_key,
      sold_quantity,
      ammount_paid,
      sale_id_dd
   )
   SELECT
      -- Use default error codes for invalid dimension records
      NVL(product_key, pck_error_codes.c_load_invalid_dim_record_key),
      NVL(store_key, pck_error_codes.c_load_invalid_dim_record_key),
      NVL(promo_key, pck_error_codes.c_load_invalid_dim_record_key),
      NVL(date_key, pck_error_codes.c_load_invalid_dim_record_key),
      NVL(time_key, pck_error_codes.c_load_invalid_dim_record_key),
      NVL(customer_key, pck_error_codes.c_load_invalid_dim_record_key),
      clean.quantity,
      clean.ammount_paid,
      clean.sale_id
   FROM
      t_clean_linesofsale clean
      -- Join with product dimension; exclude expired products
      LEFT JOIN t_dim_product
         ON clean.product_id = product_natural_key
         AND t_dim_product.is_expired_version = 'NO'
      -- Join with store dimension; exclude expired stores
      LEFT JOIN t_dim_store
         ON clean.store_id = store_natural_key
         AND t_dim_store.is_expired_version = 'NO'
      -- Join with promotion dimension
      LEFT JOIN t_dim_promotion
         ON clean.promo_id = promo_natural_key
      -- Join with date dimension using formatted date
      LEFT JOIN t_dim_date
         ON TO_CHAR(clean.line_date, 'dd/mm/yyyy') = date_full_date
      -- Join with time dimension using formatted time
      LEFT JOIN t_dim_time
         ON TO_CHAR(clean.line_date, 'hh24:mi:ss') = time_full_time
      -- Join with customer dimension; exclude expired customers
      LEFT JOIN t_dim_customer
         ON clean.customer_id = customer_natural_key
         AND t_dim_customer.is_expired_version = 'NO';
END;
```

### `main`

```sql
PROCEDURE main (
   p_load_dates      BOOLEAN,   -- Flag to control loading of date dimensions
   p_init_dimensions BOOLEAN    -- Flag to control initialization of dimensions
) IS
BEGIN
   -- Step 1: Load 'DATE' Dimensions
   IF p_load_dates THEN
      -- Load time dimension data
      load_dim_time;
   END IF;

   -- Load or update the date dimension, including weather status
   load_dim_date(p_load_dates);

   -- Step 2: Initialize Dimensions (if required)
   IF p_init_dimensions THEN
      -- Initialize any necessary dimension data
      init_dimensions;
   END IF;

   -- Step 3: Load Dimensions
   -- Load data for various dimensions
   load_dim_customer;
   load_dim_product;
   load_dim_promotion;
   load_dim_store;

   -- Step 4: Load Fact Table Data
   load_fact_table;

   -- Step 5: Commit the transaction to persist changes
   COMMIT;
END;
```
