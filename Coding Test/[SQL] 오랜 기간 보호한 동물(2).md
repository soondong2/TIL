# Today I Learned - 2022/11/06 Sun

# 오랜 기간 보호한 동물(2)
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/59411
- 난이도 : Level3
<br>

## 풀이
```sql
SELECT
    ANIMAL_ID,
    NAME
FROM (SELECT
        I.ANIMAL_ID,
        I.NAME,
        DATEDIFF(O.DATETIME, I.DATETIME) AS 보호기간
      FROM ANIMAL_INS AS I INNER JOIN ANIMAL_OUTS AS O
        USING(ANIMAL_ID)) AS subtable
ORDER BY 보호기간 DESC
LIMIT 2;
```
