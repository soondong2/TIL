# Today I Learned - 2022/11/06

# 중성화 여부 파악하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/59409
- 난이도 : Level2
<br>

## 풀이
```sql
SELECT
    ANIMAL_ID,
    NAME,
    (CASE
        WHEN SEX_UPON_INTAKE REGEXP 'Neutered|Spayed' THEN 'O'
    ELSE 'X'
    END) AS SEX_UPON_INTAKE
FROM ANIMAL_INS
ORDER BY ANIMAL_ID ASC
```
