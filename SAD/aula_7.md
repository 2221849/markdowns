# Decision Support Systems

## Lesson 7

Let's initiate the transformation process and monitor the outcomes:

```sql
-- Run the main transformation process in PCK_TRANSFORM
BEGIN
    PCK_TRANSFORM.main(FALSE);
END;
/

-- Check the ETL log to observe the results
SELECT * FROM T_LOG_ETL;
```

Now, let's focus on the execution of the `pck_transform.SCREEN_PRODUCT_DIMENSIONS` screen, which is the only one currently implemented.

### `SCREEN_PRODUCT_DIMENSIONS`

This procedure aims to detect data quality issues in the dimensions of products recorded in the `t_data_products` table, following specific business rules. It logs any identified issues without discarding the problematic data.

The cursor, `products_with_problems`, selects rows from the `t_data_products` table where data quality issues are found according to these criteria:

- **Rule 1:** If the `width`, `height`, or `depth` fields are `NULL` and the `pack_type` requires dimensions (as indicated in the `t_lookup_pack_dimensions` table), the row is flagged as problematic.
- **Rule 2:** If any of the `width`, `height`, or `depth` fields are greater than or equal to zero, but the `pack_type` should not have dimensions (according to `t_lookup_pack_dimensions`), it is also marked as an issue.

The `t_lookup_pack_dimensions` table serves to determine whether a specific `pack_type` is expected to have dimensions, based on the `has_dimensions` flag.
