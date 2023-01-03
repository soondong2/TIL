# Today I Learned - 2023/1/3 Tue

# Department Top Three Salaries
- 출처 : https://leetcode.com/problems/department-top-three-salaries/
- 난이도 : Hard
<br>
  
## 풀이
```sql
WITH output AS(
    SELECT
        D.name AS Department,
        E.name AS Employee,
        E.salary AS Salary,
        DENSE_RANK() OVER(PARTITION BY D.name ORDER BY E.salary DESC) AS salary_rank
    FROM Employee AS E INNER JOIN Department AS D ON E.departmentId = D.id
)

SELECT Department, Employee, Salary FROM output WHERE salary_rank IN (1, 2, 3);
```
