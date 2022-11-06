# Today I Learned - 2022/11/06 Sun

# 보호소에서 중성화한 동물
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/59045
- 난이도 : Level4
<br>

## 풀이
```sql
SELECT
    I.ANIMAL_ID,
    I.ANIMAL_TYPE,
    I.NAME
FROM ANIMAL_INS AS I INNER JOIN ANIMAL_OUTS AS O
    USING(ANIMAL_ID)
WHERE I.SEX_UPON_INTAKE REGEXP 'Intact'
    AND (O.SEX_UPON_OUTCOME REGEXP 'Spayed'
        OR O.SEX_UPON_OUTCOME REGEXP 'Neutered')
ORDER BY I.ANIMAL_ID ASC;
```
