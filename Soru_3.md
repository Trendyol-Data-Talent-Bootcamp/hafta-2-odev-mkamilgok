### Soru 3) "sample.pageview": tablosunda 1 gün içerisinde trendyol.com a gelen tüm ziyaretlerin logu var.

Denedim ama pek beceremedim malesef. Yine de uğraştığım query'yi koymak istedim:

```
with minute_user as(
SELECT timestamp_trunc(view_ts,minute) as minute,
       hll_count.extract(hll_count.init(deviceid, 24)) approx_user_count
FROM `dsmbootcamp.sample.pageview`
GROUP BY minute
ORDER BY minute)

SELECT minute,
       SUM(approx_user_count) 
              OVER(
                  ORDER BY UNIX_SECONDS(minute) 
                  RANGE BETWEEN 240 PRECEDING 
                  AND CURRENT ROW) as approx_active_user,
FROM minute_user
```
