# Today I Learned - 2022/12/02 Fri

# Fix Names in a Table
- 출처 : https://leetcode.com/problems/fix-names-in-a-table/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT
    user_id,
    CONCAT(UPPER(SUBSTRING(name, 1, 1)), LOWER(SUBSTRING(name, 2))) AS name
FROM Users
ORDER BY user_id ASC;
```
