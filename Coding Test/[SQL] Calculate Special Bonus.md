# Today I Learned - 2022/12/06 Tue

# Calculate Special Bonus
- 출처 : https://leetcode.com/problems/calculate-special-bonus/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT
    employee_id,
    (CASE
        WHEN MOD(employee_id, 2) = 1 AND name REGEXP '^[^M]' THEN salary
        ELSE 0
    END) AS bonus
FROM Employees
ORDER BY employee_id ASC;
```
