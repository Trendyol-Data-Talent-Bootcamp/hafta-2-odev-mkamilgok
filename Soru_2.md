### Soru 2) 1980’den itibaren herhangi bir spor grubunda üst üste 3 veya daha fazla madalya almış atletleri bulalım

```
SELECT DISTINCT A.Athlete
FROM `dsmbootcamp.kamil_gok.summer_medals` as A 
      INNER JOIN `dsmbootcamp.kamil_gok.summer_medals` as B 
          ON A.Athlete = B.Athlete 
      INNER JOIN`dsmbootcamp.kamil_gok.summer_medals` as C
          ON A.Athlete = C.Athlete
WHERE C.Year >= 1980 AND A.Year = B.Year + 4 AND B.Year = C.Year + 4
ORDER BY A.Athlete

```
