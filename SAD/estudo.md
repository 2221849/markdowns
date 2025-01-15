# **Decision Support Systems**

## **Steps to Add a New Dimension**

### **Extraction**

#### **1. Choose the Extraction Method**

You can extract data using one of the following methods:

- **From a view (table)**: Use `table_extract` or `table_extract_non_incremental`.
- **From a file (e.g., CSV)**: Use `file_extract`.
- **From a web source**: Use `web_extract`.

#### **2. Prepare the DSA Tables**

For `file_extract`, two tables are required:

1. **`_NEW` Table**: Holds incoming data.
2. **`_OLD` Table**: Preserves the previous state for comparison.

##### **SQL Commands to Create the Tables**

- **Create the main DSA table**:

  ```sql
  CREATE TABLE T_DATA (
    column1 DataType,
    column2 DataType,
    -- Add additional columns as needed
    REJECTED_BY_SCREEN CHAR DEFAULT(0)
  );
  ```

- **Create the `_OLD` table**:

  ```sql
  CREATE TABLE T_DATA_OLD AS SELECT * FROM T_DATA_NEW;
  ```

#### **3. Update the Extraction Package**

1. **Initialize new tables in `initialize_extractions_table`** of `PCK_EXTRACT`:

- Add cleanup logic for new tables.

1. **Call the extract method in `PCK_EXTRACT.main`**:

- For `file_extract`, pass `_NEW` and `_OLD` table paths.
- For `table_extract` or `web_extract`, configure appropriately.

#### **4. Validation Steps**

```sql
EXEC PCK_EXTRACT.main(TRUE);
SELECT * FROM T_LOG_ETL; -- Check ETL log for errors
SELECT * FROM T_DATA; -- Verify extracted data
```

### **Transformation**

#### **1. Define a Screen (If Required)**

Update `T_TEL_SCREEN`:

```sql
INSERT INTO T_TEL_SCREEN (
   SCREEN_NAME,
   SCREEN_CLASS,
   SCREEN_DESCRIPTION
)
VALUES (
   'SCREEN_NAME',
   'SCREEN_CLASS',
   'SCREEN_DESCRIPTION'
);
```

#### **2. Add a New Source (If Applicable)**

Update `T_TEL_SOURCE`:

```sql
INSERT INTO T_TEL_SOURCE (
   SOURCE_FILE_NAME,
   SOURCE_HOST_IP,
   SOURCE_HOST_OS,
   SOURCE_DESCRIPTION
)
VALUES (
   'new_file_name.csv',
   '172.22.21.58',
   'Windows 10',
   'Description of the file source'
);
```

#### **3. Define or Update Cleaning Table**

Create a cleaning table or add attributes as required:

```sql
CREATE TABLE T_CLEAN (
   column1 DataType,
   column2 DataType,
   ...
);
```

#### **4. Validate Transformation Steps**

```sql
EXEC PCK_TRANSFORM.main(TRUE);
SELECT * FROM V_DATA_WITH_PROBLEMS; -- View issues
SELECT * FROM T_CLEAN; -- Validate cleaned data
```

### **Load**

#### **1. Load Methods**

The load method may only use **SCD1**, **SCD1 + SCD2**, or **SCD1 + SCD2 + SCD3**.

**For SCD1 Only:**

```sql
PROCEDURE load_dim IS
BEGIN
  MERGE INTO T_DIM DIM
  USING (
    SELECT ... -- Attributes from T_CLEAN (excluding IS_EXPIRED_VERSION)
    FROM T_CLEAN
  ) CLEAN
  ON (DIM.NATURAL_KEY = CLEAN.ID)

  WHEN MATCHED THEN
    UPDATE SET ... -- Map attributes in T_DIM to T_CLEAN (excluding keys)

  WHEN NOT MATCHED THEN
    INSERT (
      ... -- Attributes in T_DIM
      )
    VALUES (
      SEQ_DIM.NEXTVAL,
      ... -- Attributes in T_CLEAN
      );
END;
```

**For SCD1 + SCD2 (Products Example):**

```sql
PROCEDURE load_dim IS
  CURSOR PRODUCTS_CURSOR IS
    SELECT ... -- All attributes from T_CLEAN_PRODUCTS;
     -- Declare variables for PK and SCD2
  FOR REC IN PRODUCTS_CURSOR LOOP
    BEGIN
      SELECT ... -- PK and SDC2 attributes
      INTO ... -- Variables for PK and SCD2
      FROM T_DIM_PRODUCT
      WHERE ... -- NATURAL_KEY = REC.ID AND IS_EXPIRED_VERSION = 'NO';

      IF ... -- If at least one variable SCD2 has changed
      THEN
        -- Mark the existing version as expired
        UPDATE T_DIM_PRODUCT
        SET IS_EXPIRED_VERSION = 'YES'
        WHERE ...; -- PK = V_KEY

        -- Insert the new version of the product
        INSERT INTO T_DIM_PRODUCT (...)
        VALUES (
          -- SEQ_DIM.NEXTVAL
          -- REC.ID
          -- ...
          -- 'NO'
          );
      ELSE
        -- If no SCD2 attributes changed, update SCD1 attributes
        UPDATE T_DIM_PRODUCT
        SET ... -- SDC1 attributes
        WHERE ...; -- PK = V_KEY
      END IF;

    EXCEPTION
      WHEN NO_DATA_FOUND THEN
        -- If no active version exists, insert as a new product
        INSERT INTO T_DIM_PRODUCT (...) VALUES (...);
    END;
  END LOOP;
END;
```

**For SCD1 + SCD2 + SCD3 (Customers Example):**

```sql
PROCEDURE load_dim_customer IS
  CURSOR CUSTOMERS_CURSOR IS
    SELECT ... -- All attributes from T_CLEAN_CUSTOMERS;
    -- Declare variables for PK, SCD2 and SCD3
  FOR REC IN CUSTOMERS_CURSOR LOOP
    BEGIN
      SELECT ... -- PK, SDC2 and SCD3 attributes
      INTO ... -- Variables for PK, SCD2 and SCD3
      FROM T_DIM_CUSTOMER WHERE ...; -- NATURAL_KEY = REC.ID AND IS_EXPIRED_VERSION = 'NO';

      -- Check if the SCD3 attribute has changed
      v_gender_old := NULL;
      IF rec.gender <> v_gender THEN
        -- Store the old gender value
        v_gender_old := v_gender;
      END IF;

      IF ... -- If at least one variable SCD2 has changed
      THEN
        -- Mark the existing version as expired
        UPDATE T_DIM_CUSTOMER
        SET IS_EXPIRED_VERSION = 'YES'
        WHERE ...; -- PK = V_KEY

        -- Insert the new version of the customer
        INSERT INTO T_DIM_CUSTOMER VALUES (...);
      ELSE
        -- If no SCD2 attributes changed, update SCD1 and SCD3 attributes
        UPDATE T_DIM_CUSTOMER
        SET ... -- SDC1 and SCD3 attributes
        WHERE ...; -- PK = V_KEY
      END IF;

    EXCEPTION
      WHEN NO_DATA_FOUND THEN
      -- If no active version exists, insert as a new customer
        INSERT INTO T_DIM_CUSTOMER VALUES (...);
    END;
  END LOOP;
END;
```
