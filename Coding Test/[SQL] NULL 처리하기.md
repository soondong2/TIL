# Today I Learned - 2022/11/06 Sun

# NULL 처리하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/59410
- 난이도 : Level2
<br>

## 풀이
```sql
SELECT
    ANIMAL_TYPE,
    COALESCE(NAME, 'No name') AS NAME,
    SEX_UPON_INTAKE
FROM ANIMAL_INS;

```
