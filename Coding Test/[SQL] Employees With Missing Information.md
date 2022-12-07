# Today I Learned - 2022/12/07 Wed

# Employees With Missing Information
- 출처 : https://leetcode.com/problems/employees-with-missing-information/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT *
FROM(
    (SELECT E1.employee_id
    FROM Employees AS E1 LEFT OUTER JOIN Salaries AS S1 ON E1.employee_id = S1.employee_id
    WHERE S1.employee_id IS NULL)
    UNION ALL
    (SELECT S2.employee_id
    FROM Employees AS E2 RIGHT OUTER JOIN Salaries AS S2 ON E2.employee_id = S2.employee_id
    WHERE E2.employee_id IS NULL)
) AS result
ORDER BY employee_id ASC;
```
