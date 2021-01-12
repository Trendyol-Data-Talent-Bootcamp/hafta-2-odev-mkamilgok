### Soru 1) 1980’den itibaren spor grubu bazında en çok madalya alan 1. 3. 5. ülkeyi bulalım

```
with rank_table as(with medal_count_table as(SELECT Sport, Country, COUNT(1) AS medal_count 
FROM `dsmbootcamp.sample.summer_medals`
WHERE Sport IS NOT NULL 
GROUP BY Sport, Country 
ORDER BY Sport, medal_count DESC)

SELECT *, ROW_NUMBER() OVER(PARTITION BY  Sport ORDER BY medal_count DESC) AS rank
FROM medal_count_table
ORDER BY rank)

SELECT DISTINCT Sport,
                (SELECT T.Country
                 FROM rank_table as T
                 WHERE T.Sport = S.Sport AND T.rank = 1
                ) as first_ranked,
                (SELECT T.Country
                 FROM rank_table as T
                 WHERE T.Sport = S.Sport AND T.rank = 3
                ) as third_ranked,
                (SELECT T.Country
                 FROM rank_table as T
                 WHERE T.Sport = S.Sport AND T.rank = 5
                ) as fifth_ranked
FROM rank_table as S
ORDER BY Sport

```
