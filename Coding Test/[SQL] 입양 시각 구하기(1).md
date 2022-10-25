# Today I Learned - 2022/10/25 Tue

# 입양 시각 구하기(1)
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/59412
- 난이도 : Level2
<br>

## 풀이
```sql
SELECT HOUR(DATETIME) AS HOUR, COUNT(*) AS COUNT
FROM ANIMAL_OUTS
GROUP BY HOUR(DATETIME)
HAVING HOUR BETWEEN 9 AND 19
ORDER BY HOUR ASC;
```
