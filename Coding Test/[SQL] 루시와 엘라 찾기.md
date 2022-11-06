# Today I Learned - 2022/11/06 Sun

# 루시와 엘라 찾기

- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/59046
- 난이도 : Level2
<br>

## 풀이
```sql
SELECT
    ANIMAL_ID,
    NAME,
    SEX_UPON_INTAKE
FROM ANIMAL_INS
WHERE NAME IN ('Lucy', 'Ella', 'Pickle', 'Rogan', 'Sabrina', 'Mitty')
```
