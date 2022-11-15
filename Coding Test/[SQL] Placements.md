# Today I Learned - 2022/11/15 Tue

# Placements
- 출처 : https://www.hackerrank.com/challenges/placements/problem?isFullScreen=true
- 난이도 : Intermediate(Medium)
<br>

## 풀이
```sql
SELECT S.Name
FROM Students AS S
    INNER JOIN Packages AS P1 ON S.ID = P1.ID
    INNER JOIN Friends AS F ON F.ID = S.ID
    INNER JOIN Packages AS P2 ON F.Friend_ID = P2.ID
WHERE P1.Salary < P2.Salary
ORDER BY P2.Salary ASC;
```
