# Today I Learned - 2022/10/11 Tue

# 아픈 동물 찾기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/59036
<br>

## 풀이
```sql
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE INTAKE_CONDITION = 'Sick'
ORDER BY ANIMAL_ID ASC;
```
