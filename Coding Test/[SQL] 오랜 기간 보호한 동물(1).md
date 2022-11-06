# Today I Learned - 2022/11/06 Sun

# 오랜 기간 보호한 동물(1)
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/59044
- 난이도 : Level3
<br>

## 풀이
```sql
SELECT
    I.NAME,
    I.DATETIME
FROM ANIMAL_INS AS I LEFT OUTER JOIN ANIMAL_OUTS AS O
    USING(ANIMAL_ID)
WHERE O.DATETIME IS NULL
ORDER BY I.DATETIME ASC
LIMIT 3;
```
