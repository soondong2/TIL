# Today I Learned - 2022/11/06 Sun

# 없어진 기록 찾기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/59042
- 난이도 : Level3
<br>

## 풀이
```sql
SELECT
    O.ANIMAL_ID,
    O.NAME
FROM ANIMAL_INS AS I RIGHT OUTER JOIN ANIMAL_OUTS AS O
    USING(ANIMAL_ID)
WHERE I.DATETIME IS NULL AND O.DATETIME IS NOT NULL
ORDER BY O.ANIMAL_ID ASC;
```
