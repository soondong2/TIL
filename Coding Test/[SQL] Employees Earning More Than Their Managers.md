# Today I Learned - 2022/11/17 Thur

# Employees Earning More Than Their Managers
- 출처 : https://leetcode.com/problems/employees-earning-more-than-their-managers/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT E1.name AS Employee
FROM Employee AS E1 LEFT OUTER JOIN Employee AS E2 ON E1.managerID = E2.id
WHERE E1.salary > E2.salary
```
