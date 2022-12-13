# Today I Learned - 2022/12/13 Tue

# Department Highest Salary
- 출처 : https://leetcode.com/problems/department-highest-salary/
- 난이도 : Medium
<br>

## 풀이
```sql
SELECT Department, Employee, Salary
FROM
    (SELECT
        D.name AS Department,
        E.name AS Employee,
        E.Salary AS Salary,
        RANK() OVER(PARTITION BY D.name ORDER BY E.salary DESC)AS salary_rank
    FROM Employee AS E INNER JOIN Department AS D ON E.departmentId = D.id) AS sub
WHERE salary_rank = 1
```
