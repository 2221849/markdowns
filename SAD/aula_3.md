# Decision Support Systems

## Lesson 3

### Objective

Utilize the non-generic procedures `table_extract_produtos` and `table_extract_promocoes` to complete the `table_extract` procedure.

The completed code should resemble the following:

```sql
PROCEDURE table_extract (
    p_source_table VARCHAR2,
    p_attributes_src VARCHAR2,
    p_attributes_dest VARCHAR2,
    p_DSA_table VARCHAR2
) IS 
    v_end_date TIMESTAMP;
    v_start_date t_info_extractions.LAST_TIMESTAMP % TYPE;
    v_sql VARCHAR2(1000);

BEGIN
    pck_log.write_log(
        '  Extracting data ["TABLE_EXTRACT (' || UPPER(p_source_table) || ')"]'
    );

    pck_log.rowcount(p_DSA_table, 'Before');

    -- Logs the initial row count of the destination table.
    -- 1st OPERATION: Clear the destination table
    v_sql := 'DELETE FROM ' || p_DSA_table;
    pck_log.write_log('    1st OPERATION: ' || v_sql);
    EXECUTE IMMEDIATE v_sql;

    -- 2nd OPERATION: Retrieve the last extracted record's date from the source table
    v_sql := 'SELECT last_timestamp ' || 
             'FROM t_info_extractions ' || 
             'WHERE UPPER(source_table_name) = ''' || UPPER(p_source_table) || '''';

    pck_log.write_log('    2nd OPERATION: ' || v_sql);
    EXECUTE IMMEDIATE v_sql INTO v_start_date;

    -- If this is the first extraction, replace NULL with C_OLDEST_DATE
    IF v_start_date IS NULL THEN 
        v_start_date := C_OLDEST_DATE;
    END IF;

    -- 3rd OPERATION: Identify the last record to be extracted from the source table
    v_sql := 'SELECT MAX(SRC_LAST_CHANGED) ' || 
             'FROM ' || p_source_table || ' ' || 
             'WHERE SRC_LAST_CHANGED > :v_start_date';

    pck_log.write_log('    3rd OPERATION: ' || v_sql);
    pck_log.write_log('    v_start_date: ' || v_start_date);
    EXECUTE IMMEDIATE v_sql INTO v_end_date USING v_start_date;
    pck_log.write_log('    v_end_date: ' || v_end_date);

    -- 4th OPERATION: Extract records from the source table to the corresponding DSA table
    IF (v_end_date IS NOT NULL) THEN
        v_sql := 'INSERT INTO ' || p_DSA_table || ' (' || p_attributes_dest || ') ' || 
                 'SELECT ' || p_attributes_src || ' FROM ' || p_source_table || ' ' || 
                 'WHERE SRC_LAST_CHANGED > :v_start_date AND SRC_LAST_CHANGED <= :v_end_date';

        pck_log.write_log('    4th OPERATION: ' || v_sql);
        EXECUTE IMMEDIATE v_sql USING v_start_date, v_end_date;

        -- 5th OPERATION: Update the table t_info_extractions
        v_sql := 'UPDATE t_info_extractions ' || 
                 'SET last_timestamp = :v_end_date ' || 
                 'WHERE UPPER(source_table_name) = ''' || UPPER(p_source_table) || '''';

        pck_log.write_log('    5th OPERATION: ' || v_sql);
        EXECUTE IMMEDIATE v_sql USING v_end_date;
    END IF;

    pck_log.write_log('    Done!');
    pck_log.rowcount(p_DSA_table, 'After');

    -- Logs the final row count of the destination table
EXCEPTION
    WHEN OTHERS THEN 
        pck_log.write_uncomplete_task_msg;
        RAISE e_extraction;
END;
```

### Next Steps

Uncomment `table_extract` from `pck_extract.main` and initialize `t_info_extractions`.

**Test the `PCK_EXTRACT` Procedure:**

```sql
SELECT * FROM T_DATA_PRODUCTS;
BEGIN
    PCK_EXTRACT.main(TRUE);
END;
/
SELECT * FROM T_LOG_ETL;
```

The `TRUE` parameter in `PCK_EXTRACT.main(TRUE)`; indicates a full load, meaning it extracts and loads all available data from the source system to the target system; if set to `FALSE`, it will only extract and load data that has changed since the last extraction, thereby minimizing resource usage and processing time.
