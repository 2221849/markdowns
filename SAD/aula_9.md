# Decision Support Systems

## Lesson 9

### `LOAD_DIM_PROMOTION`

The `LOAD_DIM_PROMOTION` process demonstrates how to load data into a promotions dimension table (`T_DIM_PROMOTION`) by comparing source data from `T_CLEAN_PROMOTIONS`. It uses the SQL `MERGE` statement to handle both inserts and updates efficiently.

```sql
MERGE INTO T_DIM_PROMOTION TARGET USING(
  SELECT
    id,
    NAME,
    start_date,
    end_date,
    reduction,
    on_outdoor,
    on_tv
  FROM
    T_CLEAN_PROMOTIONS
) SOURCE ON (TARGET.promo_natural_Key = SOURCE.ID)
WHEN MATCHED THEN
UPDATE
SET
  TARGET.promo_name = SOURCE.name,
  TARGET.promo_start_date = SOURCE.start_date,
  TARGET.promo_end_date = SOURCE.end_date,
  TARGET.promo_red_price = SOURCE.reduction,
  TARGET.promo_board = SOURCE.on_outdoor,
  TARGET.promo_advertise = SOURCE.on_tv
  WHEN NOT MATCHED THEN
INSERT
  (
    TARGET.promo_key,
    TARGET.promo_natural_Key,
    TARGET.promo_name,
    TARGET.promo_start_date,
    TARGET.promo_end_date,
    TARGET.promo_red_price,
    TARGET.promo_board,
    TARGET.promo_advertise
  )
VALUES
  (
    seq_dim_promotion.NEXTVAL,
    SOURCE.id,
    SOURCE.name,
    SOURCE.start_date,
    SOURCE.end_date,
    SOURCE.reduction,
    SOURCE.on_outdoor,
    SOURCE.on_tv
  );
```
