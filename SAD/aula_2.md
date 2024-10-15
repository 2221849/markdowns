# Decision Support Systems

## Lesson 2

### First Task - `T_EXT_MANAGERS`

Create a new object `T_EXT_MANAGERS` responsible for presenting data from the `managers.csv` file. Examine the `managers.csv` file to identify the **separator of the values**, **data types of the columns**, paying special attention to dates and the location of the file. Use the `T_EXT_STORES` procedure as a reference.

The `T_EXT_MANAGERS` table definition can look like this:

```sql
CREATE TABLE T_EXT_MANAGERS(
    reference       CHAR(6),
    manager_name    VARCHAR2(50),
    manager_since   DATE
)
ORGANIZATION EXTERNAL
(
    TYPE oracle_loader
    DEFAULT DIRECTORY src_files
    ACCESS PARAMETERS
    (
        RECORDS DELIMITED BY newline
        BADFILE 'managers_2221849.bad'
        DISCARDFILE 'managers_2221849.dis'
        LOGFILE 'managers_2221849.log'
        SKIP 7
        FIELDS TERMINATED BY ';' OPTIONALLY ENCLOSED BY '"' MISSING FIELD VALUES ARE NULL
        (
            reference       CHAR(6),
            phone_nrs       CHAR(50),
            manager_name    CHAR(50),
            nif             CHAR(50),
            manager_since   DATE 'yyyy/mm/dd',
            is_first        CHAR(3)
        )
    )
    LOCATION ('managers.csv')
)
REJECT LIMIT UNLIMITED;
```

**Key Points**:

1. **Data Separator**: In this case, it's a semicolon `;` as shown in the `FIELDS TERMINATED BY ';'` clause.
2. **Column Data Types**:
   - `reference` is a `CHAR(6)`
   - `manager_name` is a `VARCHAR2(50)`
   - `manager_since` is a `DATE` with format `'yyyy/mm/dd'`
3. **File Location**: The file `managers.csv` is located in the `src_files` directory.
4. **Skip Rows**: Skip the first 7 rows (possibly headers or irrelevant data) as indicated by `SKIP 7`.

Once the external table is created, you can test it by running:

```sql
SELECT * FROM T_EXT_MANAGERS;
```

This query will allow you to see if the data from `managers.csv` is correctly loaded into the external table.

### Second Task - `file_extract`

Create a generic procedure `file_extract` based on the procedure `file_extract_lojas`. The purpose of this procedure is to manage the extraction of data from external files and store it in the appropriate destination tables.

The procedure might look like this:

```sql
PROCEDURE file_extract (
    p_external_table VARCHAR2,  -- NAME OF EXTERNAL TABLE
    p_attributes_src VARCHAR2,  -- ATTRIBUTES FROM SOURCE TABLE (EXTERNAL TABLE)
    p_attributes_dest VARCHAR2, -- NAME OF ATTRIBUTES ON DESTINATION TABLE
    p_dsa_table_new VARCHAR2,   -- NAME OF AUXILIARY TABLE (NEW DATA)
    p_dsa_table_old VARCHAR2    -- NAME OF DESTINATION TABLE (OLD DATA)
) IS
   v_sql  VARCHAR2(1000); -- Variable for dynamic SQL commands
BEGIN
   PCK_LOG.write_log('  Extracting data ["FILE_EXTRACT ('||UPPER(p_external_table)||')"]');      
   PCK_LOG.rowcount(p_dsa_table_new,'Before');    -- Log the row count before the operation

   -- OPERATION 1: Delete all rows from the old table
   v_sql:='DELETE FROM '||p_dsa_table_old;
   PCK_LOG.write_log('    STEP 1: '||v_sql);
   EXECUTE IMMEDIATE v_sql;

   -- OPERATION 2: Preserve previous data from the new table into the old table
   v_sql:='INSERT INTO '||p_dsa_table_old||' SELECT * FROM '||p_dsa_table_new;
   PCK_LOG.write_log('    STEP 2: '||v_sql);
   EXECUTE IMMEDIATE v_sql;

   -- OPERATION 3: Clear the new table to receive new data from the file
   v_sql:='DELETE FROM '||p_dsa_table_new;
   PCK_LOG.write_log('    STEP 3: '||v_sql);
   EXECUTE IMMEDIATE v_sql;

   -- OPERATION 4: Load new data from the external table
   v_sql:='INSERT INTO '||p_dsa_table_new||'('||p_attributes_dest||')'||'SELECT '||p_attributes_src||' FROM '||p_external_table;
   PCK_LOG.write_log('    STEP 4: '||v_sql);
   EXECUTE IMMEDIATE v_sql;

   -- Log the success of the extraction
   PCK_LOG.write_log('    Done!');
   PCK_LOG.rowcount(p_dsa_table_new,'After');    -- Log the row count after the operation
EXCEPTION
   WHEN OTHERS THEN
      PCK_LOG.write_uncomplete_task_msg;
      RAISE e_extraction;
END;
```

**Key Steps**:

1. **Step 1**: Delete all records from the old table (`p_dsa_table_old`).
2. **Step 2**: Insert the data from the new table (`p_dsa_table_new`) into the old table (`p_dsa_table_old`) to preserve previous extractions.
3. **Step 3**: Delete all records from the new table (`p_dsa_table_new`) to prepare for fresh data.
4. **Step 4**: Insert new data into the new table from the external file.

### Changes on `PCK_EXTRACT.main`

- Comment out the initialization of the extraction table `t_info_extractions`.
- Comment out all lines where the `table_extract` procedure is invoked.
- Add calls to the file_extract procedure for the managers tables

```sql
file_extract(
    't_ext_managers',                       -- External table
    'reference,manager_name,manager_since', -- Source attributes
    'reference,manager_name,manager_since', -- Destination attributes
    't_data_managers_new',                  -- Auxiliar data table
    't_data_managers_old'                   -- Destination data table
);
```

Ensure that the attribute list in the third argument of `file_extract` matches the corresponding attributes of the destination table specified in the last argument.

### Testing the `PCK_EXTRACT.file_extract` Procedure

Once the procedure is created, test it with the following steps:

```sql
-- Check the old data
SELECT * FROM T_DATA_MANAGERS_OLD;

-- Execute the extraction procedure
BEGIN
    PCK_EXTRACT.main(TRUE);
END;
/

-- Check the new data
SELECT * FROM T_DATA_MANAGERS_NEW;

-- Analyze the log entries
SELECT * FROM T_LOG_ETL;
```

This test checks if the data is properly transferred and logs any issues or successful steps during the extraction process.
