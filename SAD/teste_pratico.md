# Decision Support Systems

## **Extraction**

### **Source File: `coupons.csv`**

The file contains coupon data in the following format:

```csv
Ficheiro de Cupões;;;;;;
Export manager 2.0.1;;;;;;
08-jan-2024 02:04 A.M;;;;;;
;;;;;;
id;code;name;discount;start_date;end_date;type
1;123456781;Maçã Campina;25;02-01-2024;07-01-2024;1
2;123456782;Bolachas;25;02-01-2024;07-01-2024;2
3;123456783;Batatas Fritas;50;02-01-2024;14-01-2024;2
4;123456784;Marisco Congelado;25;02-01-2024;07-01-2024;2
5;123456785;Massas Secas e Arroz;15;02-01-2024;07-01-2024;2
6;123456786;Sumos e Refrigerantes;35;07-01-2024;02-02-2024;2
7;123456787;Compra em Loja;150;15-01-2024;28-01-2024;0
```

### **External Table Creation**

```sql
CREATE TABLE T_EXT_COUPONS (
  CODE NUMBER,
  NAME VARCHAR2(100),
  DISCOUNT NUMBER,
  START_DATE DATE,
  END_DATE DATE,
  TYPE NUMBER
) ORGANIZATION EXTERNAL (
  TYPE oracle_loader
  DEFAULT DIRECTORY src_files
  ACCESS PARAMETERS (
    RECORDS DELIMITED BY NEWLINE
    BADFILE 'coupons.bad'
    DISCARDFILE 'coupons.dis'
    LOGFILE 'coupons.log'
    SKIP 5
    FIELDS TERMINATED BY ';'
    OPTIONALLY ENCLOSED BY '"'
    MISSING FIELD VALUES ARE NULL (
      ID CHAR(1),
      CODE CHAR(9),
      NAME CHAR(100),
      DISCOUNT CHAR(3),
      START_DATE DATE 'dd-mm-yyyy',
      END_DATE DATE 'dd-mm-yyyy',
      TYPE CHAR(1)
    )
  )
  LOCATION ('coupons.csv')
) REJECT LIMIT UNLIMITED;
```

### **Data Staging**

```sql
CREATE TABLE T_DATA_COUPONS_NEW (
    CODE NUMBER,
    NAME VARCHAR2(100),
    DISCOUNT NUMBER,
    START_DATE DATE,
    END_DATE DATE,
    TYPE NUMBER,
    REJECTED_BY_SCREEN CHAR DEFAULT(0)
);
```

```sql
CREATE TABLE T_DATA_COUPONS_OLD AS SELECT * FROM T_DATA_COUPONS_NEW;
```

### **Data Cleaning**

Clean `T_DATA_COUPON_NEW` and `T_DATA_COUPON_OLD` on `initialize_extractions_table`:

```sql
...
DELETE FROM t_data_coupons_new;
DELETE FROM t_data_coupons_old;
pck_log.write_log('      Done!');
```

### **Extracting Data**

```sql
file_extract (
  'T_EXT_COUPONS',
  'CODE,NAME,DISCOUNT,START_DATE,END_DATE,TYPE',
  'CODE,NAME,DISCOUNT,START_DATE,END_DATE,TYPE',
  'T_DATA_COUPONS_NEW',
  'T_DATA_COUPONS_OLD'
);
```

### **Update Line of Sale Table**

```sql
ALTER TABLE T_DATA_LINESOFSALE ADD COUPON_ID NUMBER(10);
```

```sql
table_extract(
  'VIEW_LINHASVENDA@DBLINK_SADSB',
  'SRC_ID,SRC_SALE_ID,SRC_PRODUCT_ID,SRC_QUANTITY,SRC_COUPON_ID,SRC_LINE_DATE,SRC_AMMOUNT_PAID',
  'ID,SALE_ID,PRODUCT_ID,QUANTITY,COUPON_ID,LINE_DATE,AMMOUNT_PAID',
  'T_DATA_LINESOFSALE'
);
```

### **Extraction Validation**

```sql
BEGIN
    PCK_EXTRACT.main(TRUE); -- Load data with full extraction
END;
/
SELECT * FROM T_LOG_ETL; -- Check ETL log for errors
SELECT * FROM T_DATA_COUPONS_NEW; -- Verify loaded data
SELECT * FROM T_DATA_COUPONS_OLD; -- Verify loaded data
```

## **Transformation**

### **Register New Source and Screen**

```sql
INSERT INTO T_TEL_SOURCE (
    SOURCE_FILE_NAME,
    SOURCE_HOST_IP,
    SOURCE_HOST_OS,
    SOURCE_DESCRIPTION
)
VALUES (
    'COUPONS.CSV',
    '172.22.21.58',
    'Windows 10',
    'Ficheiro contendo informação dos coupons'
);
```

```sql
INSERT INTO T_TEL_SCREEN (
    SCREEN_NAME,
    SCREEN_CLASS,
    SCREEN_DESCRIPTION
)
VALUES (
    'SCREEN_COUPON',
    'CORREÇÃO',
    'Disconto ou datas inválidas'
);
```

### **Prepare Cleaned Tables**

```sql
ALTER TABLE T_CLEAN_LINESOFSALE ADD COUPON_ID INTEGER;
```

```sql
CREATE TABLE T_CLEAN_COUPONS (
    CODE NUMBER,
    NAME VARCHAR2(100),
    DISCOUNT NUMBER,
    DURATION_DAYS NUMBER,
    TYPE_DESCRIPTION VARCHAR2(10)
);
```

### **Procedure: `screen_coupon`**

```sql
PROCEDURE screen_coupon (
  p_iteration_key t_tel_iteration.iteration_key % TYPE,
  p_source_key t_tel_source.source_key % TYPE,
  p_screen_order t_tel_schedule.screen_order % TYPE
) IS -- SEARCH FOR EXTRACTED PRODUCTS CONTAINING PROBLEMS
CURSOR coupons_with_problems IS
SELECT
  ROWID
FROM
  T_DATA_COUPONS_NEW
WHERE
  REJECTED_BY_SCREEN = '0'
  AND (
    DISCOUNT < 0
    OR DISCOUNT > 100
  )
  OR(END_DATE < START_DATE);

i PLS_INTEGER := 0;

v_screen_name VARCHAR2(30) := 'screen_coupon';

BEGIN
  pck_log.write_log(
    '  Starting SCREEN ["' || UPPER(v_screen_name) || '"] with order #' || p_screen_order || ''
  );

FOR rec IN coupons_with_problems
LOOP
  -- RECORDS THE ERROR IN THE TRANSFORMATION ERROR LOGGER AND * REJECTS THE LINE *
  error_log(
    v_screen_name,
    SYSDATE,
    p_source_key,
    p_iteration_key,
    rec.rowid
  );

-- SETS THE SOURCE RECORD AS 'REJECTED'
UPDATE
  T_DATA_COUPONS_NEW
SET
  rejected_by_screen = '1'
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
  WHEN OTHERS THEN pck_log.write_uncomplete_task_msg;

RAISE e_transformation;

END;
```

Make sure `screen_coupon` is public

```sql
PROCEDURE screen_coupon (
  p_iteration_key t_tel_iteration.iteration_key % TYPE,
  p_source_key t_tel_source.source_key % TYPE,
  p_screen_order t_tel_schedule.screen_order % TYPE
);
```

### **Procedure: `transform_lineofsale`**

Update `transform_lineofsale` (new attribute in `T_CLEAN_LINESOFSALE`)

```sql
PROCEDURE transform_linesofsale IS BEGIN
  pck_log.write_log('  Transforming data ["TRANSFORM_LINESOFSALE"]');

INSERT INTO
  T_CLEAN_LINESOFSALE (
    ID,
    SALE_ID,
    PRODUCT_ID,
    QUANTITY,
    AMMOUNT_PAID,
    LINE_DATE,
    PROMO_ID,
    STORE_ID,
    CUSTOMER_ID,
    COUPON_ID
  )
SELECT
  LINESOFSALE.ID,
  LINESOFSALE.SALE_ID,
  LINESOFSALE.PRODUCT_ID,
  LINESOFSALE.QUANTITY,
  LINESOFSALE.AMMOUNT_PAID,
  LINESOFSALE.LINE_DATE,
  PROMOTIONS.PROMO_ID,
  SALES.STORE_ID,
  SALES.CUSTOMER_ID,
  COUPONS.CODE
FROM
  T_DATA_LINESOFSALE LINESOFSALE
  JOIN T_DATA_SALES SALES ON LINESOFSALE.SALE_ID = SALES.ID
  LEFT JOIN T_DATA_LINESOFSALEPROMOTIONS PROMOTIONS ON (
    LINESOFSALE.ID = PROMOTIONS.LINE_ID
    AND PROMOTIONS.REJECTED_BY_SCREEN = '0'
  )
  LEFT JOIN T_DATA_COUPONS_NEW COUPONS ON LINESOFSALE.COUPON_ID = COUPONS.CODE
WHERE
  LINESOFSALE.REJECTED_BY_SCREEN = '0'
  AND SALES.REJECTED_BY_SCREEN = '0'
  AND COUPONS.REJECTED_BY_SCREEN = '0';

pck_log.write_log('    Done!');

EXCEPTION
  WHEN NO_DATA_FOUND THEN pck_log.write_log('    Found no lines to transform', '    Done!');

WHEN OTHERS THEN pck_log.write_uncomplete_task_msg;

RAISE e_transformation;

END;
```

### **Procedure: `transform_coupons`**

```sql
PROCEDURE transform_coupons IS BEGIN
  pck_log.write_log('  Transforming data ["TRANSFORM_COUPONS"]');

INSERT INTO
  T_CLEAN_COUPONS (
    CODE,
    NAME,
    DISCOUNT,
    DURATION_DAYS,
    TYPE_DESCRIPTION
  )
SELECT
  SUBTRACTED.CODE,
  SUBTRACTED.NAME,
  SUBTRACTED.DISCOUNT,
  SUBTRACTED.END_DATE - SUBTRACTED.START_DATE,
  CASE
    SUBTRACTED.TYPE
    WHEN 0 THEN 'STORE'
    WHEN 1 THEN 'PRODUCT'
    WHEN 2 THEN 'CATEGORY'
    WHEN 3 THEN 'SECTION'
  END
FROM
  (
    SELECT
      CODE,
      NAME,
      DISCOUNT,
      START_DATE,
      END_DATE,
      TYPE,
      REJECTED_BY_SCREEN
    FROM
      T_DATA_COUPONS_NEW
    WHERE
      REJECTED_BY_SCREEN = '0'
    MINUS
    SELECT
      CODE,
      NAME,
      DISCOUNT,
      START_DATE,
      END_DATE,
      TYPE,
      REJECTED_BY_SCREEN
    FROM
      T_DATA_COUPONS_OLD
  ) SUBTRACTED
WHERE
  SUBTRACTED.REJECTED_BY_SCREEN = '0';

pck_log.write_log('    Done!');

EXCEPTION
  WHEN NO_DATA_FOUND THEN pck_log.write_log('    Found no lines to transform', '    Done!');

WHEN OTHERS THEN pck_log.write_uncomplete_task_msg;

RAISE e_transformation;

END;
```

### **Updates in Main**

Clean the `T_CLEAN_COUPONS` table:

```sql
DELETE FROM T_CLEAN_COUPONS;
```

Call the `transform_coupons` procedure:

```sql
...
transform_coupons;
```

### **Transformation Validation**

```sql
BEGIN
    PCK_TRANSFORM.main(TRUE); -- Full transformation process
END;
/
SELECT * FROM V_DATA_WITH_PROBLEMS; -- View records with issues
SELECT * FROM V_LAST_ITERATION_INFO; -- Check iteration details
SELECT * FROM T_LOG_ETL; -- Verify ETL logs
SELECT * FROM T_CLEAN_LINESOFSALE; -- Validate cleaned data
SELECT * FROM T_CLEAN_COUPONS; -- Validate cleaned data
```

## **Load**

### **Dimension Table Creation**

```sql
CREATE TABLE T_DIM_COUPON (
    COUPON_KEY NUMBER(12),
    COUPON_NATURAL_KEY NUMBER,
    COUPON_NAME VARCHAR2(100 CHAR),
    COUPON_DISCOUNT_PERCENTAGE NUMBER(3),
    COUPON_DURATION_DAYS NUMBER(3),
    COUPON_TYPE VARCHAR2(10 CHAR),
    IS_EXPIRED_VERSION VARCHAR2(3 CHAR),
    CONSTRAINT PK_TDIMCOUPON_KEY PRIMARY KEY (COUPON_KEY)
);
```

```sql
CREATE SEQUENCE SEQ_COUPON_KEY;
```

### **Initialize Coupon Dimension**

```sql
INSERT INTO
  T_DIM_COUPON (
    COUPON_KEY,
    COUPON_NATURAL_KEY,
    COUPON_NAME,
    COUPON_DISCOUNT_PERCENTAGE,
    COUPON_DURATION_DAYS,
    COUPON_TYPE,
    IS_EXPIRED_VERSION
  )
VALUES
  (
    PCK_ERROR_CODES.C_LOAD_INVALID_DIM_RECORD_KEY,
    PCK_ERROR_CODES.C_LOAD_INVALID_DIM_RECORD_NKEY,
    'INVALID COUPON',
    NULL,
    NULL,
    NULL,
    'NO'
  );
```

### **Load Procedure**

Implement `load_dim_coupon` with SCD2 on `COUPON_TYPE`

```sql
PROCEDURE load_dim_coupon IS -- Cursor to fetch cleaned product data
CURSOR coupons_cursor IS
SELECT
  CODE,
  NAME,
  DISCOUNT,
  DURATION_DAYS,
  TYPE_DESCRIPTION
FROM
  T_CLEAN_COUPONS;

-- Statistic counters
i INTEGER := 0;

V_NEW_COUPONS INTEGER := 0;

V_NEW_VERSIONS INTEGER := 0;

V_OLD_VERSIONS INTEGER := 0;

-- Coupon Key
V_COUPON_KEY T_DIM_COUPON.COUPON_KEY % TYPE;

-- Variables for SCD checking
V_COUPON_TYPE T_DIM_COUPON.COUPON_TYPE % TYPE;

BEGIN
  PCK_LOG.WRITE_LOG('  Loading data ["LOAD_DIM_COUPON"]');

PCK_LOG.ROWCOUNT('T_DIM_COUPON');

-- Loop through each record in the cleaned coupons data
FOR REC IN coupons_cursor LOOP
  -- SEARCHES THE COUPON IN THE DIMENSION BY SELECTING SCD2 ATTRIBUTES
  BEGIN
    SELECT
      COUPON_KEY,
      COUPON_TYPE
    INTO
      V_COUPON_KEY,
      V_COUPON_TYPE
    FROM
      T_DIM_COUPON
    WHERE
      COUPON_NATURAL_KEY = REC.CODE
      AND IS_EXPIRED_VERSION = 'NO';

-- Check if any SCD2 attributes have changed
IF REC.TYPE_DESCRIPTION != V_COUPON_TYPE THEN -- Mark the existing version as expired
UPDATE
  T_DIM_COUPON
SET
  IS_EXPIRED_VERSION = 'YES'
WHERE
  COUPON_KEY = V_COUPON_KEY;

-- Insert the new version of the coupon
INSERT INTO
  T_DIM_COUPON (
    COUPON_KEY,
    COUPON_NATURAL_KEY,
    COUPON_NAME,
    COUPON_DISCOUNT_PERCENTAGE,
    COUPON_DURATION_DAYS,
    COUPON_TYPE
  )
VALUES
  (
    SEQ_DIM_COUPON.NEXTVAL,
    REC.CODE,
    REC.NAME,
    REC.DISCOUNT,
    REC.DURATION_DAYS,
    REC.TYPE_DESCRIPTION
  );

-- Increment new versions counter
V_NEW_VERSIONS := V_NEW_VERSIONS + 1;

ELSE -- If no SCD2 attributes changed, update SCD1 attributes
UPDATE
  T_DIM_COUPON
SET
  COUPON_NAME = REC.NAME,
  COUPON_DISCOUNT_PERCENTAGE = REC.DISCOUNT,
  COUPON_DURATION_DAYS = REC.DURATION_DAYS
WHERE
  COUPON_KEY = V_COUPON_KEY;

-- Increment old versions counter
V_OLD_VERSIONS := V_OLD_VERSIONS + 1;

END IF;

EXCEPTION
  WHEN NO_DATA_FOUND THEN -- If no active version exists, insert as a new coupon
INSERT INTO
  T_DIM_COUPON (
    COUPON_KEY,
    COUPON_NATURAL_KEY,
    COUPON_NAME,
    COUPON_DISCOUNT_PERCENTAGE,
    COUPON_DURATION_DAYS,
    COUPON_TYPE,
    IS_EXPIRED_VERSION
  )
VALUES
  (
    SEQ_DIM_COUPON.NEXTVAL,
    REC.CODE,
    REC.NAME,
    REC.DISCOUNT,
    REC.DURATION_DAYS,
    REC.TYPE_DESCRIPTION,
    'NO'
  );

-- Increment new coupons counter
V_NEW_COUPONS := V_NEW_COUPONS + 1;

END;
END LOOP;

-- RECORDS SOME STATISTICS CONCERNING LOADED COUPONS
PCK_LOG.WRITE_LOG(
  '    ' || v_OLD_VERSIONS || ' old coupon(s) updated in SCD1 attributes',
  '    ' || V_NEW_VERSIONS || ' old coupon(s) got new version(s) (old have expired)'
);

PCK_LOG.WRITE_LOG(
  '    ' || V_NEW_COUPONS || ' new coupon(s) found and loaded',
  '    Done!'
);

PCK_LOG.ROWCOUNT('T_DIM_COUPON');

EXCEPTION
  WHEN OTHERS THEN PCK_LOG.WRITE_UNCOMPLETE_TASK_MSG;

RAISE e_load;

END;
```

Call `load_dim_coupon` in main

```sql
...
load_dim_coupon;
load_fact_table;
```

Change `T_FACT_LINEOFSALE` with new key

```sql
ALTER TABLE T_FACT_LINEOFSALE ADD COUPON_KEY INTEGER;

ALTER TABLE T_FACT_LINEOFSALE
ADD CONSTRAINT FK_TFACTLINEOFSALE_COUPONKEY
    FOREIGN KEY (COUPON_KEY)
    REFERENCES T_DIM_COUPON(COUPON_KEY);

ALTER TABLE T_FACT_LINEOFSALE DROP CONSTRAINT PK_TFACTLINEOFSALE_PK;

ALTER TABLE T_FACT_LINEOFSALE
ADD CONSTRAINT PK_TFACTLINEOFSALE_PK PRIMARY KEY (DATE_KEY, TIME_KEY, PRODUCT_KEY, SALE_ID_DD, COUPON_KEY);
```

```sql
PROCEDURE load_fact_table IS V_SOURCE_LINES INTEGER;

BEGIN
  PCK_LOG.WRITE_LOG('  Loading data ["LOAD_FACT_TABLE"]');

-- JUST FOR STATISTICS
SELECT
  COUNT(*) INTO V_SOURCE_LINES
FROM
  T_CLEAN_LINESOFSALE;

INSERT INTO
  T_FACT_LINEOFSALE (
    PRODUCT_KEY,
    STORE_KEY,
    COUPON_KEY, -- * new
    PROMO_KEY,
    DATE_KEY,
    TIME_KEY,
    CUSTOMER_KEY,
    SOLD_QUANTITY,
    AMMOUNT_PAID,
    SALE_ID_DD
  )
SELECT
  NVL(
    PRODUCT_KEY,
    PCK_ERROR_CODES.C_LOAD_INVALID_DIM_RECORD_KEY
  ),
  NVL(
    STORE_KEY,
    PCK_ERROR_CODES.C_LOAD_INVALID_DIM_RECORD_KEY
  ),
  NVL(
    COUPON_KEY, -- * new
    PCK_ERROR_CODES.C_LOAD_INVALID_DIM_RECORD_KEY
  ),
  NVL(
    PROMO_KEY,
    PCK_ERROR_CODES.C_LOAD_INVALID_DIM_RECORD_KEY
  ),
  NVL(
    DATE_KEY,
    PCK_ERROR_CODES.C_LOAD_INVALID_DIM_RECORD_KEY
  ),
  NVL(
    TIME_KEY,
    PCK_ERROR_CODES.C_LOAD_INVALID_DIM_RECORD_KEY
  ),
  NVL(
    CUSTOMER_KEY,
    PCK_ERROR_CODES.C_LOAD_INVALID_DIM_RECORD_KEY
  ),
  CLEAN.QUANTITY,
  CLEAN.AMMOUNT_PAID,
  CLEAN.SALE_ID
FROM
  T_CLEAN_LINESOFSALE CLEAN -- não considerar produtos expirados
  LEFT JOIN T_DIM_PRODUCT ON (
    CLEAN.PRODUCT_ID = PRODUCT_NATURAL_KEY
    AND T_DIM_PRODUCT.IS_EXPIRED_VERSION = 'NO'
  ) -- não considerar lojas expiradas
  LEFT JOIN T_DIM_STORE ON (
    CLEAN.STORE_ID = STORE_NATURAL_KEY
    AND T_DIM_STORE.IS_EXPIRED_VERSION = 'NO'
  )
  LEFT JOIN T_DIM_PROMOTION ON CLEAN.PROMO_ID = PROMO_NATURAL_KEY
  LEFT JOIN T_DIM_DATE ON TO_CHAR(CLEAN.LINE_DATE, 'DD/MM/YYYY') = DATE_FULL_DATE
  LEFT JOIN T_DIM_TIME ON TO_CHAR(CLEAN.LINE_DATE, 'HH24:MI:SS') = TIME_FULL_TIME
  LEFT JOIN T_DIM_COUPON ON CLEAN.COUPON_ID = COUPON_NATURAL_KEY -- * new
  LEFT JOIN T_DIM_CUSTOMER ON (
    CLEAN.CUSTOMER_ID = CUSTOMER_NATURAL_KEY
    AND T_DIM_CUSTOMER.IS_EXPIRED_VERSION = 'NO' -- NÃO CONSIDERAR CLIENTES EXPIRADOS
  );

PCK_LOG.WRITE_LOG(
  '    ' || SQL % ROWCOUNT || ' fact(s) loaded',
  '    Done!'
);

EXCEPTION
  WHEN NO_DATA_FOUND THEN PCK_LOG.WRITE_LOG(
    '    No facts generated from ' || V_SOURCE_LINES || ' source lines-of-sale'
  );

WHEN OTHERS THEN PCK_LOG.WRITE_UNCOMPLETE_TASK_MSG;

RAISE e_load;

END;
```

### **Load Validation**

```sql
BEGIN
    PCK_LOAD.main(TRUE, TRUE);
END;
/

SELECT * FROM T_DIM_COUPON; -- Verify dimensional data
SELECT * FROM T_FACT_LINEOFSALE; -- Validate related data
SELECT * FROM T_LOG_ETL; -- Check logs for errors
```
