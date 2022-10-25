# Today I Learned - 2022/10/25 Tue

# 동명 동물 수 찾기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/59041
- 난이도 : Level2
<br>

## 풀이
```sql
SELECT NAME, COUNT(*) AS COUNT
FROM ANIMAL_INS
GROUP BY NAME
HAVING COUNT(NAME) >= 2 AND NAME IS NOT NULL
ORDER BY NAME ASC;
```
