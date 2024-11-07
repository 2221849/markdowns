# Decision Support Systems

## Lesson 5

- Analyze the architecture map
- Analyze the logical map

When comparing the database tables with those in the logical map, it is observed that the tables `T_DATA_CUSTOMERS` and `T_DATA_CUSTOMERS_REG` do not exist in the database. Therefore, these tables need to be created and extracted, with the extraction of `T_DATA_CUSTOMERS_REG` being non-incremental, as indicated in the logical map.

Use the script located at `Moodle\SAD\Aulas Práticas\Plataforma ETL^2.24.0\Materiais\etl^2_2.24.0_aulas\scripts_extract\CREATE_data_tables.sql` as a base to create the tables:

```sql
CREATE TABLE t_data_customers(
  id INTEGER,
  card_number VARCHAR2(20),
  NAME VARCHAR2(40),
  address VARCHAR2(60),
  location VARCHAR2(60),
  district VARCHAR2(40),
  zip_code VARCHAR2(8),
  phone_nr NUMBER(9),
  gender CHAR(10),
  age NUMBER(3),
  marital_status CHAR(1),
  rejected_by_screen CHAR DEFAULT(0)
);

CREATE TABLE t_data_customers_reg(
  card_number VARCHAR2(20),
  customer_type VARCHAR2(10),
  rejected_by_screen CHAR DEFAULT(0)
);
```

To extract data from the tables, use the following commands:

```sql
table_extract(
  'view_clientes@dblink_sadsb',
  'src_id,src_card_number,src_name,src_address,src_location,src_district,src_zip_code,src_phone_nr,src_gender,src_age,src_marital_status',
  'id,card_number,name,address,location,district,zip_code,phone_nr,gender,age,marital_status',
  't_data_customers'
);

table_extract_non_incremental(
  'view_registos@dblink_sadsb',
  't_data_customers_reg',
  'src_card_number,src_customer_type',
  'card_number,customer_type'
);
```

Since the extraction process for customers is incremental, the procedure `initialize_extractions_table` needs to be updated.

Upon reviewing the attributes of all the tables, it is noted that the table `T_DATA_SALES` is missing the `customer_id` field. Therefore, the table needs to be modified:

```sql
ALTER TABLE t_data_sales
ADD customer_id INTEGER;
```

Next, extract the data for `T_DATA_SALES`:

```sql
table_extract(
  'view_vendas@dblink_sadsb',
  'src_id,src_store_id,src_customer_id',
  'id,store_id,customer_id',
  't_data_sales'
);
```

After the extraction process, set the parameter to `TRUE` to initialize the support structures:

```sql
BEGIN
    PCK_EXTRACT.main(TRUE);
END;
/
```

To verify if everything is correct, run the following queries:

```sql
SELECT * FROM T_LOG_ETL;

SELECT * FROM T_DATA_CUSTOMERS;
SELECT * FROM T_DATA_CUSTOMERS_REG;
SELECT * FROM T_DATA_SALES;
```
