# Decision Support Systems

## Lesson 8

- **Continue the Transformation Process**
  - Build the transformation method to implement the transformations defined for data from IPMA. Include the created method in the execution flow for the transformation phase.
- **Testing**
- **[Extra] Apply the Transformation Process to Customers**

### `TRANSFORM_CELSIUS` Procedure

```sql
-- *********************************************************
-- * TRANSFORMATION OF FACTS ACCORDING TO LOGICAL DATA MAP *
-- *********************************************************
PROCEDURE transform_celsius IS
BEGIN
  -- Log start of transformation process
  pck_log.write_log('  Transforming data ["TRANSFORM_LINESOFSALE"]');

  -- Insert transformed data into target table T_CLEAN_CELSIUS
  INSERT INTO T_CLEAN_CELSIUS (forecast_date, temperature_status)
  SELECT
    forecast_date,
    CASE
      WHEN AVG((t_min + t_max) / 2) < 4 THEN 'COLD'
      WHEN AVG((t_min + t_max) / 2) < 10 THEN 'FRESH'
      WHEN AVG((t_min + t_max) / 2) < 25 THEN 'NICE'
      ELSE 'HOT'
    END AS temperature_status
  FROM
    t_data_celsius C
  GROUP BY
    forecast_date;

  -- Log end of transformation
  pck_log.write_log('    Done!');

EXCEPTION
  WHEN NO_DATA_FOUND THEN
    -- Log case where no data was available for transformation
    pck_log.write_log('    Found no lines to transform');
    pck_log.write_log('    Done!');

  WHEN OTHERS THEN
    -- Log any other errors and raise a transformation error
    pck_log.write_uncomplete_task_msg;
    RAISE e_transformation;

END;
```

**Explanation:**

This procedure, `TRANSFORM_CELSIUS`, transforms temperature data by categorizing it into status labels (`COLD`, `FRESH`, `NICE`, or `HOT`) based on the average of `t_min` and `t_max` temperatures for each forecast date. The transformed data is then inserted into `T_CLEAN_CELSIUS`.

**Key Notes:**

1. **Logging**: Logs are included at the start and end of the procedure to track the transformation process.
2. **Error Handling**: Catches the `NO_DATA_FOUND` exception and logs a specific message. Other exceptions are handled generally by logging an incomplete task message and raising a transformation error.

**Don't Forget!**

Ensure that this procedure is **called** in the appropriate part of the ETL (Extraction, Transformation, Load) process, and clean up the `T_DATA_CELSIUS` table after the transformation is complete
