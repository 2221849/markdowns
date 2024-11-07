# Decision Support Systems

## Lesson 4

```sql
web_extract(
'http://api.ipma.pt/open-data/forecast/meteorology/cities/daily/hp-daily-forecast-day0.json',
't_data_celsius',
'SELECT
    t.data_.forecastDate,
    jt.globalIdLocal,
    jt.tMin,
    jt.tMax
FROM
    t_data_json_temp t,
    JSON_TABLE(
        t.data_,
        ''$.data[*]''
        COLUMNS(
            globalIdLocal INTEGER PATH ''$.globalIdLocal'',
            tMin INTEGER PATH ''$.tMin'',
            tMax INTEGER PATH ''$.tMax''
        )
    ) AS jt',
'forecast_date,id_local,t_min,t_max'
);
```
