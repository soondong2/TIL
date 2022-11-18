# Today I Learned - 2022/11/18 Fri

# Duplicate Emails
- 출처 : https://leetcode.com/problems/duplicate-emails/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT email
FROM Person
GROUP BY email
HAVING COUNT(*) >= 2
```
