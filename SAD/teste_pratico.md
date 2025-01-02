# Decision Support Systems

## EXTRACTION

### "coupons.csv"

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

```sql
CREATE TABLE T_EXT_COUPONS (
  CODE NUMBER,
  NAME VARCHAR2(100),
  DISCOUNT NUMBER,
  START_DATE DATE,
  END_DATE DATE,
  TYPE CHAR(1)
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

```sql
ALTER TABLE T_DATA_LINESOFSALE ADD COUPON_ID NUMBER(10);
```

Clean `T_DATA_COUPON_NEW` and `T_DATA_COUPON_OLD` with `initialize_extractions_table`

```sql
-- ...
DELETE FROM t_data_coupons_new;
DELETE FROM t_data_coupons_old;
pck_log.write_log('      Done!');
```

Call `file_extract` on coupons

```sql
-- EXTRAÇÃO DINÁMICA
--...
file_extract (
  'T_EXT_COUPONS',
  'ID,SALE_ID,PRODUCT_ID,QUANTITY,LINE_DATE,AMMOUNT_PAID,REJECTED_BY_SCREEN,COUPON_ID',
  'ID,CODE,NAME,DISCOUNT,START_DATE,END_DATE,TYPE,REJECTED_BY_SCREEN',
  'T_DATA_COUPONS_NEW',
  'T_DATA_COUPONS_OLD'
);
```

**Extraction Validation Steps**:

```sql
BEGIN
    PCK_EXTRACT.main(TRUE); -- Load data with full extraction
END;
/
SELECT * FROM T_LOG_ETL; -- Check ETL log for errors
SELECT * FROM T_DATA_COUPONS_NEW; -- Verify loaded data
SELECT * FROM T_DATA_COUPONS_OLD; -- Verify loaded data
```

## TRANSFORMATION

1. Add new source to `T_TEL_SOURCE`
2. Add new screen in `T_TEL_SCREEN`
3. Schedule the new screen in `T_TEL_SCHEDULE`
4. Make sure `screen_coupon` is public (add in outer main)

```sql
ALTER TABLE T_CLEAN_LINESOFSALE ADD coupon_id INTEGER;
```

```sql
CREATE TABLE T_CLEAN_COUPONS (
    id NUMBER PRIMARY KEY,
    code VARCHAR2(50) NOT NULL,
    name VARCHAR2(255) NOT NULL,
    discount NUMBER NOT NULL,
    duration_days NUMBER NOT NULL,
    type_description VARCHAR2(8)
);

```

- Implement `screen_coupon`
- Update `transform_lineofsales` (new attribute in `T_CLEAN_LINESOFSALE`)
- Update main:
  - `DELETE FROM T_CLEAN_COUPONS;`
  - `transform_coupons`

## LOAD

```sql
ALTER TABLE T_DIM_LINESOFSALE ADD coupon_key INTEGER;
```

```sql
CREATE TABLE T_DIM_COUPON (
    coupon_key NUMBER PRIMARY KEY,
    coupon_natural_key NUMBER NOT NULL UNIQUE,
    coupon_name VARCHAR2(255) NOT NULL,
    coupon_discount_percentage NUMBER NOT NULL,
    coupon_duration_days NUMBER NOT NULL,
    coupon_type NUMBER NOT NULL,
    is_expired_version VARCHAR2(3)
);
```

```sql
CREATE SEQUENCE seq_coupon_key;
```

- Create init_dimensions
- Implement SCD
- Change `T_FACT_LINEOFSALE` with new key

```sql
ALTER TABLE T_CLEAN_LINESOFSALE ADD coupon_id INTEGER;
```

- Call `load_coupon` in main
