# Today I Learned - 2022/12/12 Mod

# Second Highest Salary
- 출처 : https://leetcode.com/problems/second-highest-salary/
- 난이도 : Medium
<br>

## 풀이
```sql
SELECT MAX(salary) AS SecondHighestSalary
FROM Employee
WHERE salary < (SELECT MAX(salary) FROM Employee);
```
