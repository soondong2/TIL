# Today I Learned - 2022/11/08 Tue

# Weather Observation Station 20
- 출처 : https://www.hackerrank.com/challenges/weather-observation-station-20/problem?isFullScreen=true
- 난이도 : Intermediate(Medium)
<br>

## 풀이
```sql
SET @idx := -1;

SELECT ROUND(AVG(result.LAT_N), 4) AS MEDIAN
FROM (SELECT
        @idx := @idx + 1 AS IDX,
      LAT_N
      FROM STATION
      ORDER BY LAT_N ASC) AS result
WHERE result.IDX IN (FLOOR(@idx / 2), CEIL(@idx / 2));
```
