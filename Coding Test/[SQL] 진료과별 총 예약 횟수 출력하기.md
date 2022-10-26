# Today I Learned - 2022/10/26 Wed

# 진료과별 총 예약 횟수 출력하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/132202
- 난이도 : Level2
<br>

## 풀이
```sql
SELECT MCDP_CD AS '진료과코드', COUNT(*) AS '5월예약건수'
FROM APPOINTMENT
WHERE SUBSTRING(APNT_YMD, 1, 7) = '2022-05'
GROUP BY MCDP_CD
ORDER BY 5월예약건수 ASC, 진료과코드 ASC;
```
