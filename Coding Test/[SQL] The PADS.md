# Today I Leanred - 2022/11/07 Mon

# The PADS
- 출처 : https://www.hackerrank.com/challenges/the-pads/problem?isFullScreen=true
- 난이도 : Basic(Medium)
<br>

## 풀이
```sql
SELECT CONCAT(Name, '(', SUBSTRING(Occupation, 1, 1), ')') AS result
FROM OCCUPATIONS
ORDER BY result ASC;

SELECT CONCAT('There are a total of ', COUNT(*), ' ', LOWER(Occupation), 's.')
FROM OCCUPATIONS
GROUP BY Occupation
ORDER BY COUNT(*) ASC, Occupation ASC
```
