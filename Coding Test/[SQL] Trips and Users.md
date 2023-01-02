# Today I Learned - 2023/1/1

# Trips and Users
- 출처 : https://leetcode.com/problems/trips-and-users/description/
- 난이도 : Hard
<br>

## 풀이
```sql
SELECT
    request_at AS Day,
    ROUND(SUM(status != 'completed') / COUNT(*), 2) AS 'Cancellation Rate'
FROM Trips
WHERE
    request_at BETWEEN '2013-10-01' AND '2013-10-03'
    AND client_id NOT IN (SELECT users_id FROM Users WHERE banned = 'Yes')
    AND driver_id NOT IN (SELECT users_id FROM Users WHERE banned = 'Yes')
GROUP BY request_at
```
