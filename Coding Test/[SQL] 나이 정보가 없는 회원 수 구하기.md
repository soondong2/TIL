# Today I Learned - 2022/11/06 Sun

# 나이 정보가 없는 회원 수 구하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/131528
- 난이도 : Level1
<br>

## 풀이
```sql
SELECT COUNT(*)
FROM USER_INFO
WHERE AGE IS NULL;
```
