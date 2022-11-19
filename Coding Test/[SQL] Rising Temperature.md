# Today I Learned - 2022/11/19 Sat

# Rising Temperature
- 출처 : https://leetcode.com/problems/rising-temperature/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT today.id
FROM Weather AS today INNER JOIN Weather AS yesterday
    ON today.recordDate = DATE_ADD(yesterday.recordDate, INTERVAL 1 DAY)
WHERE today.temperature > yesterday.temperature
```
