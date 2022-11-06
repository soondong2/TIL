# Today I Learned - 2022/11/06 Sun

# 이름에 el이 들어가는 동물 찾기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/59047
- 난이도 : Level2
<br>

## 풀이
```sql
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE NAME REGEXP 'el' AND ANIMAL_TYPE = 'Dog'
ORDER BY NAME ASC
```
