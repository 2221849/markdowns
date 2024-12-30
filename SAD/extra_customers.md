# **Decision Support Systems: Extra Customers**

## **Extraction Phase**

### **Objective**

Extract raw customer data from the source table `view_clientes@dblink_sadsb` and insert it into the staging table `t_data_customers`.

### **Implementation**

#### **Staging Tables**

Ensure that the staging tables T_DATA_CUSTOMERS and T_DATA_CUSTOMERS_REG exist. If not, create them as follows:

```sql
CREATE TABLE T_DATA_CUSTOMERS(
  ID INTEGER,
  CARD_NUMBER VARCHAR2(20),
  NAME VARCHAR2(40),
  ADDRESS VARCHAR2(60),
  LOCATION VARCHAR2(60),
  DISTRICT VARCHAR2(40),
  ZIP_CODE VARCHAR2(8),
  PHONE_NR NUMBER(9),
  GENDER CHAR(10),
  AGE NUMBER(3),
  MARITAL_STATUS CHAR(1),
  REJECTED_BY_SCREEN CHAR DEFAULT(0)
);

CREATE TABLE T_DATA_CUSTOMERS_REG(
  CARD_NUMBER VARCHAR2(20),
  CUSTOMER_TYPE VARCHAR2(10),
  REJECTED_BY_SCREEN CHAR DEFAULT(0)
);
```

#### **Data Extraction Procedure**

Use the `table_extract` procedure to move data from the source to the staging table:

```sql
table_extract(
  'view_clientes@dblink_sadsb',
  'src_id,src_card_number,src_name,src_address,src_location,src_district,src_zip_code,src_phone_nr,src_gender,src_age,src_marital_status',
  'id,card_number,name,address,location,district,zip_code,phone_nr,gender,age,marital_status',
  't_data_customers'
);
```

#### **Validation Steps**

Run the `PCK_EXTRACT` package to verify the extraction process:

```sql
SELECT * FROM VIEW_CLIENTES@DBLINK_SADSB; -- Verify source data
BEGIN
    PCK_EXTRACT.main(TRUE); -- Load data with full extraction
END;
/
SELECT * FROM T_LOG_ETL; -- Check ETL log for errors
SELECT * FROM T_DATA_CUSTOMERS; -- Verify loaded data
SELECT * FROM T_INFO_EXTRACTIONS; -- Check extraction info
```

## **Transformation Phase**

### **Objective**

Clean, standardize, and validate the extracted customer data to ensure consistency and readiness for loading into the dimensional model.

### **Implementation**

#### **Create Transformation Table**

Create the intermediate table `T_CLEAN_CUSTOMERS` to store cleaned and validated data.

```sql
CREATE TABLE T_CLEAN_CUSTOMERS(
  ID NUMBER(38),
  CARD_NUMBER VARCHAR2(20),
  NAME VARCHAR2(40),
  ADDRESS VARCHAR2(60),
  LOCATION VARCHAR2(60),
  DISTRICT VARCHAR2(40),
  ZIP_CODE VARCHAR2(8),
  PHONE_NR NUMBER(9),
  GENDER VARCHAR2(15 CHAR),
  AGE NUMBER(3),
  CUSTOMER_TYPE VARCHAR2(10 CHAR)
  MARITAL_STATUS VARCHAR2(15 CHAR),
);
```

#### **Procedure: `transform_customers`**

Transform and clean data according to the logical data map:

```sql
PROCEDURE transform_customers IS BEGIN
  pck_log.write_log('  Transforming data ["TRANSFORM_CUSTOMERS"]');

INSERT INTO
  T_CLEAN_CUSTOMERS(
    ID,
    CARD_NUMBER,
    NAME,
    ADDRESS,
    LOCATION,
    DISTRICT,
    ZIP_CODE,
    PHONE_NR,
    GENDER,
    AGE,
    MARITAL_STATUS,
    CUSTOMER_TYPE
  )
SELECT
  ID,
  R.CARD_NUMBER,
  UPPER(NAME),
  UPPER(ADDRESS),
  UPPER(LOCATION),
  UPPER(DISTRICT),
  ZIP_CODE,
  PHONE_NR,
  CASE
    UPPER(GENDER)
    WHEN 'M' THEN 'MALE'
    WHEN 'F' THEN 'FEMALE'
    ELSE 'OTHER'
  END AGE,
  CASE
    UPPER(MARITAL_STATUS)
    WHEN 'C' THEN 'MARRIED'
    WHEN 'S' THEN 'SINGLE'
    WHEN 'V' THEN 'WIDOW'
    WHEN 'D' THEN 'DIVORCED'
    ELSE 'OTHER'
  END UPPER(CUSTOMER_TYPE)
FROM
  T_DATA_CUSTOMERS C
  JOIN T_DATA_CUSTOMERS_REG R ON C.CARD_NUMBER = R.CARD_NUMBER
WHERE
  C.REJECTED_BY_SCREEN = '0' -- Only include records that have not been rejected by the screen
END;

pck_log.write_log('    Done!');

EXCEPTION
  WHEN NO_DATA_FOUND THEN pck_log.write_log('    Found no lines to transform', '    Done!');

WHEN OTHERS THEN pck_log.write_uncomplete_task_msg;

RAISE e_transformation;

END;
```

#### **Updates to `main`**

- Include a `DELETE FROM` statement to clear `T_CLEAN_CUSTOMERS`.
- Add a call to the `transform_customers` procedure.

#### **Validation Steps**

Execute the transformation procedures and verify results:

```sql
BEGIN
    PCK_TRANSFORM.main(TRUE); -- Full transformation process
END;
/
SELECT * FROM V_DATA_WITH_PROBLEMS; -- View records with issues
SELECT * FROM V_LAST_ITERATION_INFO; -- Check iteration details
SELECT * FROM T_LOG_ETL; -- Verify ETL logs
SELECT * FROM T_CLEAN_CUSTOMERS; -- Validate cleaned data
```

## **3. Loading Phase**

### **Objective**

Load the cleaned and transformed customer data into the dimensional model (`T_DIM_CUSTOMER`), applying Slowly Changing Dimensions (SCD) as necessary.

### **Implementation**

#### **Dimensional Table**

```sql
CREATE TABLE T_DIM_CUSTOMER(
  CUSTOMER_KEY NUMBER(12),
  CUSTOMER_NATURAL_KEY NUMBER(10),
  CUSTOMER_CARD_NUMBER VARCHAR2(20 CHAR),
  CUSTOMER_name VARCHAR2(40 CHAR),
  CUSTOMER_ADDRESS VARCHAR2(60 CHAR),
  CUSTOMER_LOCATION VARCHAR2(60 CHAR),
  CUSTOMER_DISTRICT VARCHAR2(40 CHAR),
  CUSTOMER_ZIP_CODE VARCHAR2(8 CHAR),
  CUSTOMER_PHONE_NR NUMBER(9),
  CUSTOMER_GENDER VARCHAR2(15 CHAR),
  CUSTOMER_AGE NUMBER(3),
  CUSTOMER_MARITAL_STATUS VARCHAR2(15 CHAR),
  CUSTOMER_TYPE VARCHAR2(20 CHAR),
  IS_EXPIRED_VERSION VARCHAR2(3 CHAR),
  CONSTRAINT PK_TDIMCUSTOMER_CUSTOMERKEY PRIMARY KEY (CUSTOMER_KEY)
);
```

#### **Load Procedure**

Implements SCD logic for detecting changes and updating the dimensional table:

```sql
PROCEDURE LOAD_DIM_CUSTOMER IS CURSOR CUSTOMERS_CURSOR IS
SELECT
  ID,
  CARD_NUMBER,
  NAME,
  ADDRESS,
  LOCATION,
  DISTRICT,
  ZIP_CODE,
  PHONE_NR,
  GENDER,
  AGE,
  MARITAL_STATUS,
  CUSTOMER_TYPE
FROM
  T_CLEAN_CUSTOMERS;

-- Counters
V_NEW_CUSTOMERS INTEGER := 0;

V_NEW_VERSIONS INTEGER := 0;

V_UPDATED_SCD1 INTEGER := 0;

-- Variables for SCD checks
V_KEY T_DIM_CUSTOMER.CUSTOMER_KEY % TYPE;

V_LOCATION T_DIM_CUSTOMER.CUSTOMER_LOCATION % TYPE;

V_DISTRICT T_DIM_CUSTOMER.CUSTOMER_DISTRICT % TYPE;

V_ZIP_CODE T_DIM_CUSTOMER.CUSTOMER_ZIP_CODE % TYPE;

V_AGE T_DIM_CUSTOMER.CUSTOMER_AGE % TYPE;

V_MARITAL_STATUS T_DIM_CUSTOMER.CUSTOMER_MARITAL_STATUS % TYPE;

V_CUSTOMER_TYPE T_DIM_CUSTOMER.CUSTOMER_TYPE % TYPE;

V_GENDER T_DIM_CUSTOMER.CUSTOMER_GENDER % TYPE;

V_GENDER_OLD T_DIM_CUSTOMER.CUSTOMER_GENDER % TYPE;

BEGIN
  PCK_LOG.WRITE_LOG('  LOADING DATA ["LOAD_DIM_CUSTOMER"]');

PCK_LOG.ROWCOUNT('T_DIM_CUSTOMER', 'BEFORE');

FOR REC IN CUSTOMERS_CURSOR
LOOP
  BEGIN
    -- Search for customer in the dimension table
    SELECT
      CUSTOMER_KEY,
      CUSTOMER_LOCATION,
      CUSTOMER_DISTRICT,
      CUSTOMER_ZIP_CODE,
      CUSTOMER_AGE,
      CUSTOMER_MARITAL_STATUS,
      CUSTOMER_TYPE,
      CUSTOMER_GENDER INTO V_KEY,
      V_LOCATION,
      V_DISTRICT,
      V_ZIP_CODE,
      V_AGE,
      V_MARITAL_STATUS,
      V_CUSTOMER_TYPE,
      V_GENDER
    FROM
      T_DIM_CUSTOMER
    WHERE
      CUSTOMER_NATURAL_KEY = REC.ID;

-- Check for SCD3 changes (CUSTOMER_GENDER)
V_GENDER_OLD := NULL;

-- Retain old value
IF REC.GENDER <> V_GENDER THEN V_GENDER_OLD := V_GENDER;

END IF;

-- Check for SCD2 changes
IF (REC.LOCATION != V_LOCATION)
OR (REC.DISTRICT != V_DISTRICT)
OR (REC.ZIP_CODE != V_ZIP_CODE)
OR (REC.AGE != V_AGE)
OR (REC.MARITAL_STATUS != V_MARITAL_STATUS)
OR (REC.CUSTOMER_TYPE != V_CUSTOMER_TYPE) THEN
UPDATE
  T_DIM_CUSTOMER
SET
  -- Mark the existing version as expired
  IS_EXPIRED_VERSION = 'YES'
WHERE
  CUSTOMER_KEY = V_KEY;

-- Insert new version of the customer
INSERT INTO
  T_DIM_CUSTOMER (
    CUSTOMER_KEY,
    CUSTOMER_NATURAL_KEY,
    CUSTOMER_CARD_NUMBER,
    CUSTOMER_NAME,
    CUSTOMER_ADDRESS,
    CUSTOMER_LOCATION,
    CUSTOMER_DISTRICT,
    CUSTOMER_ZIP_CODE,
    CUSTOMER_PHONE_NR,
    CUSTOMER_GENDER,
    CUSTOMER_GENDER_OLD,
    CUSTOMER_AGE,
    CUSTOMER_MARITAL_STATUS,
    CUSTOMER_TYPE,
    IS_EXPIRED_VERSION
  )
VALUES
  (
    SEQ_DIM_CUSTOMER.NEXTVAL,
    REC.ID,
    REC.CARD_NUMBER,
    REC.NAME,
    REC.ADDRESS,
    REC.LOCATION,
    REC.DISTRICT,
    REC.ZIP_CODE,
    REC.PHONE_NR,
    REC.GENDER,
    V_GENDER_OLD,
    REC.AGE,
    REC.MARITAL_STATUS,
    REC.CUSTOMER_TYPE,
    'NO'
  );

V_NEW_VERSIONS := V_NEW_VERSIONS + 1;

ELSE -- If no SCD2 changes, update SCD1 attributes
UPDATE
  T_DIM_CUSTOMER
SET
  CUSTOMER_CARD_NUMBER = REC.CARD_NUMBER,
  CUSTOMER_NAME = REC.NAME,
  CUSTOMER_ADDRESS = REC.ADDRESS,
  CUSTOMER_PHONE_NR = REC.PHONE_NR
WHERE
  CUSTOMER_KEY = V_KEY;

V_UPDATED_SCD1 := V_UPDATED_SCD1 + 1;

END IF;

EXCEPTION
  WHEN NO_DATA_FOUND THEN -- Insert new customer if not found
INSERT INTO
  T_DIM_CUSTOMER (
    CUSTOMER_KEY,
    CUSTOMER_NATURAL_KEY,
    CUSTOMER_CARD_NUMBER,
    CUSTOMER_NAME,
    CUSTOMER_ADDRESS,
    CUSTOMER_LOCATION,
    CUSTOMER_DISTRICT,
    CUSTOMER_ZIP_CODE,
    CUSTOMER_PHONE_NR,
    CUSTOMER_GENDER,
    CUSTOMER_GENDER_OLD,
    CUSTOMER_AGE,
    CUSTOMER_MARITAL_STATUS,
    CUSTOMER_TYPE,
    IS_EXPIRED_VERSION
  )
VALUES
  (
    SEQ_DIM_CUSTOMER.NEXTVAL,
    REC.ID,
    REC.CARD_NUMBER,
    REC.NAME,
    REC.ADDRESS,
    REC.LOCATION,
    REC.DISTRICT,
    REC.ZIP_CODE,
    REC.PHONE_NR,
    REC.GENDER,
    NULL,
    REC.AGE,
    REC.MARITAL_STATUS,
    REC.CUSTOMER_TYPE,
    'NO'
  );

V_NEW_CUSTOMERS := V_NEW_CUSTOMERS + 1;

END;

END
LOOP
;

-- Log statistics
PCK_LOG.WRITE_LOG(
  '    ' || V_UPDATED_SCD1 || ' CUSTOMER(S) UPDATED FOR SCD1 ATTRIBUTES.',
  '    ' || V_NEW_VERSIONS || ' CUSTOMER(S) WITH NEW VERSIONS DUE TO SCD2 CHANGES.',
  '    ' || V_NEW_CUSTOMERS || ' NEW CUSTOMER(S) ADDED.'
);

PCK_LOG.ROWCOUNT('T_DIM_CUSTOMER');

PCK_LOG.WRITE_LOG('    DONE!');

EXCEPTION
  WHEN OTHERS THEN PCK_LOG.WRITE_UNCOMPLETE_TASK_MSG;

RAISE E_LOAD;

END;
```

#### **Changes on `init_dimensions`**

```sql
-- 'INVALID CUSTOMER'
INSERT INTO
  T_DIM_CUSTOMER (
    CUSTOMER_KEY,
    CUSTOMER_NATURAL_KEY,
    CUSTOMER_CARD_NUMBER,
    CUSTOMER_NAME,
    CUSTOMER_ADDRESS,
    CUSTOMER_LOCATION,
    CUSTOMER_DISTRICT,
    CUSTOMER_ZIP_CODE,
    CUSTOMER_PHONE_NR,
    CUSTOMER_GENDER,
    CUSTOMER_GENDER_OLD,
    CUSTOMER_AGE,
    CUSTOMER_MARITAL_STATUS,
    IS_EXPIRED_VERSION
  )
VALUES
  (
    pck_error_codes.c_load_invalid_dim_record_key,
    pck_error_codes.c_load_invalid_dim_record_Nkey,
    NULL,
    'INVALID CUSTOMER',
    NULL,
    NULL,
    NULL,
    NULL,
    NULL,
    NULL,
    NULL,
    NULL,
    NULL,
    'NO'
  );
```

#### **Procedure: `load_fact_table`**

Update the `load_fact_table` procedure to incorporate the customer dimension.

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

## **4. Testing and Validation**

Perform the following tests:

1. **Extraction Test:**

   ```sql
   BEGIN
       PCK_EXTRACT.main(TRUE);
   END;
   ```

2. **Transformation Test:**

   ```sql
   BEGIN
       PCK_TRANSFORM.main(TRUE);
   END;
   ```

3. **Loading Test:**

   ```sql
   BEGIN
       PCK_LOAD.main(TRUE);
   END;
   ```

4. **Validation Queries:**

   ```sql
   SELECT * FROM T_DIM_CUSTOMER; -- Verify dimensional data
   SELECT * FROM T_FACT_LINEOFSALE; -- Validate related data
   SELECT * FROM T_LOG_ETL; -- Check logs for errors
   ```

## **Conclusion**

This document serves as a comprehensive guide to the ETL implementation for customer data. Each phase is detailed with SQL code, testing procedures, and validations to ensure data quality and consistency.
