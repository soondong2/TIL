# Today I Learned - 2022/11/06 Sun

# DATETIME에서 DATE로 형 변환
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/59414
- 난이도 : Level2
<br>

## 풀이
```sql
SELECT 
    ANIMAL_ID,
    NAME,
    DATE_FORMAT(DATETIME, '%Y-%m-%d')
FROM ANIMAL_INS
ORDER BY ANIMAL_ID ASC
```
