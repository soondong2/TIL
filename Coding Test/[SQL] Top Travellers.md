# Today I Learned - 2022/11/29 Tue

# Top Travellers
- 출처 : https://leetcode.com/problems/top-travellers/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT
    U.name,
    IF(R.user_id IS NULL, 0, SUM(R.distance)) AS travelled_distance 
FROM Users AS U LEFT OUTER JOIN Rides AS R ON U.id = R.user_id
GROUP BY R.user_id
ORDER BY travelled_distance DESC, U.name ASC;
```
