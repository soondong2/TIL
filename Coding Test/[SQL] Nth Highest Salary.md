# Today I Learned - 2022/12/20 Wed

# Nth Highest Salary
- 출처 : https://leetcode.com/problems/nth-highest-salary/
- 난이도 : Medium
<br>

## 풀이
```sql
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
  RETURN (
      SELECT DISTINCT(salary)
      FROM
        (SELECT 
                salary,
                DENSE_RANK() OVER(ORDER BY salary DESC) AS 'salary_rank'
        FROM Employee) AS sub
      WHERE sub.salary_rank = N
  );
END
```
