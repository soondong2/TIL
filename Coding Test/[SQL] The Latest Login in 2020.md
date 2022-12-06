# Today I Learned - 2022/12/06 Tue

# The Latest Login in 2020
- 출처 : https://leetcode.com/problems/the-latest-login-in-2020/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT user_id, MAX(time_stamp) AS last_stamp
FROM Logins
WHERE time_stamp REGEXP '2020'
GROUP BY user_id
```
