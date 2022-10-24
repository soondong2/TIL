# Today I Learned - 2022/10/24 Mon

# 12세 이하인 여자 환자 목록 출력하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/132201
- 난이도 : Level1
<br>

## 풀이
```sql
SELECT
    PT_NAME,
    PT_NO,
    GEND_CD,
    AGE,
    COALESCE(TLNO, 'NONE') AS TLNO
FROM PATIENT
WHERE AGE <= 12 AND GEND_CD = 'W'
ORDER BY AGE DESC, PT_NAME ASC;
```
