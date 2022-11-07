# Today I Learned - 2022/11/07 Mon

# Weather Observation Station 8
- 출처 : https://www.hackerrank.com/challenges/weather-observation-station-8/problem?isFullScreen=true
- 난이도 : Basic(easy)
<br>

## 풀이
```sql
SELECT DISTINCT(CITY)
FROM STATION
WHERE CITY REGEXP '^[a, e, i, o, u]' AND CITY REGEXP '[a, e, i, o, u]$';
```
