# Today I Learned - 2022/11/07 Mon

# Weather Observation Station 4
- 출처 : https://www.hackerrank.com/challenges/weather-observation-station-6/problem?isFullScreen=true
- 난이도 : Basic(easy)
<br>

## 풀이
```sql
SELECT COUNT(*) - COUNT(DISTINCT(CITY))
FROM STATION
```
