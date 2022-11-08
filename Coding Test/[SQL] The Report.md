# Today I Learned - 2022/11/08 Tue

# The Report
- 출처 : https://www.hackerrank.com/challenges/the-report/problem?isFullScreen=true
- 난이도 : Intermediate(Medium)
<br>

## 풀이
```sql
SELECT
    IF(G.Grade < 8, NULL, S.Name) AS Name,
    G.Grade,
    S.Marks
FROM Students AS S INNER JOIN Grades AS G
    ON S.Marks BETWEEN G.Min_Mark AND G.Max_Mark
ORDER BY G.Grade DESC, Name ASC, S.Marks ASC;
```
