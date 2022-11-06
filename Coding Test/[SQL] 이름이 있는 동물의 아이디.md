# Today I Learned - 2022/11/06 Sun

# 이름이 있는 동물의 아이디
- 출처 : https://school.programmers.co.kr/learn/courses/30/parts/17045
- 난이도 : Level1
<br>

## 풀이
```sql
SELECT ANIMAL_ID
FROM ANIMAL_INS
WHERE NAME IS NOT NULL
ORDER BY ANIMAL_ID ASC;
```
