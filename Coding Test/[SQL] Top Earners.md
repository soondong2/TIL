# Today I Learned - 2022/11/07 Mon

# Top Earners
- 출처 : https://www.hackerrank.com/challenges/earnings-of-employees/problem?isFullScreen=true
- 난이도 : Basic(easy)
<br>

## 풀이
```sql
SELECT
    (salary * months),
    COUNT(*)
FROM Employee
WHERE (salary * months) = (SELECT (salary * months) AS earnings
                           FROM Employee
                           ORDER BY earnings DESC
                           LIMIT 1)
GROUP BY (salary * months);
```
