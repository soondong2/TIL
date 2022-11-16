# Today I Learned - 2022/11/16 Wed

# SQL Project Planning
- 출처 : https://www.hackerrank.com/challenges/sql-projects/problem?isFullScreen=true
- 난이도 : Intermediate(Medium)
<br>

## 풀이
```sql
SET SQL_MODE = '';
SELECT A.Start_Date, MIN(B.End_Date)
FROM (SELECT Start_Date
      FROM Projects
      WHERE Start_Date NOT IN (SELECT End_Date FROM Projects)) AS A,
     (SELECT End_Date
      FROM Projects
      WHERE End_Date NOT IN (SELECT Start_Date FROM Projects)) AS B
WHERE A.Start_Date < B.End_Date
GROUP BY A.Start_Date
ORDER BY DATEDIFF(B.End_Date, A.Start_Date) ASC, A.Start_Date ASC
```
