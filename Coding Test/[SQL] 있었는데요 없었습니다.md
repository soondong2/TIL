# Today I Learned - 2022/11/06 Sun

# 있었는데요 없었습니다
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/59043
- 난이도 : Level3
<br>

## 풀이
```sql
SELECT
    I.ANIMAL_ID,
    I.NAME
FROM ANIMAL_INS AS I INNER JOIN ANIMAL_OUTS AS O
    USING(ANIMAL_ID)
WHERE I.DATETIME > O.DATETIME
ORDER BY I.DATETIME ASC;
```
