# Today I Learned - 2022/10/17 Mon

# 조건에 맞는 회원수 구하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/131535
- 난이도 : Level1
<br>

## 풀이
```sql
SELECT COUNT(*)
FROM USER_INFO
WHERE YEAR(JOINED) = 2021
    AND AGE BETWEEN 20 AND 29;
```
