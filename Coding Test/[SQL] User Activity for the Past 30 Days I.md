# Today I Learned - 2022/11/30 Wed

# User Activity for the Past 30 Days I
- 출처 : https://leetcode.com/problems/user-activity-for-the-past-30-days-i/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT 
    activity_date AS day,
    COUNT(DISTINCT(user_id)) AS active_users
FROM Activity
WHERE activity_date < '2019-07-27'
    AND DATEDIFF('2019-07-27', activity_date) < 30
GROUP BY activity_date
```
