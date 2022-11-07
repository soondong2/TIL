# Today I Learned - 2022/11/07 Mon

# Type of Triangle
- 출처 : https://www.hackerrank.com/challenges/what-type-of-triangle/problem?isFullScreen=true
- 난이도 : Basic(easy)
<br>

## 풀이
```sql
SELECT
    (CASE
        WHEN (A = B) AND (B = C) AND (A = C) THEN 'Equilateral'
        WHEN (A+B <= C) OR (B+C <= A) OR (A+C < B) THEN 'Not A Triangle'
        WHEN (A != B) AND (B != C) AND (A != C) THEN 'Scalene'
        ELSE 'Isosceles'
    END)
FROM TRIANGLES;
```
