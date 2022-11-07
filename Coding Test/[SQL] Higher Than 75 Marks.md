# Today I Learned - 2022/11/07 Mon

# Higher Than 75 Marks
- 출처 : https://www.hackerrank.com/challenges/more-than-75-marks/problem?isFullScreen=true
- 난이도 : Basic(easy)
<br>

## 풀이
```sql
SELECT Name
FROM STUDENTS
WHERE Marks > 75
ORDER BY SUBSTRING(Name, -3, 3) ASC, ID ASC;
```
