# Today I Learned - 2022/11/07 Mon

# Weather Observation Station 3
- 출처 : https://www.hackerrank.com/challenges/weather-observation-station-3/problem?isFullScreen=true
- 난이도 : Basic
<br>

## 풀이
```sql
SELECT DISTINCT(CITY)
FROM STATION
WHERE MOD(ID, 2) = 0;
```
