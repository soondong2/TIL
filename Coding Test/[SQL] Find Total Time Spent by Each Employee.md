# Today I Learned - 2022/12/04 Sun

# Find Total Time Spent by Each Employee
- 출처 : https://leetcode.com/problems/find-total-time-spent-by-each-employee/
- 난이도 : Easy
<br>

## 풀이 
```sql
SELECT event_day AS day, emp_id, SUM(total_time) AS total_time
FROM (SELECT emp_id, event_day, (out_time - in_time) AS total_time
      FROM Employees) AS sub
GROUP BY emp_id, event_day;
```
