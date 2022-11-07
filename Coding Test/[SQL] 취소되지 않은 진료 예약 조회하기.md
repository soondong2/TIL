# Today I Learned - 2022/11/07 Mon

# 취소되지 않은 진료 예약 조회하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/132204
- 난이도 : Level4
<br>

## 풀이
```sql
SELECT
    A.APNT_NO,
    P.PT_NAME,
    P.PT_NO,
    A.MCDP_CD,
    D.DR_NAME,
    A.APNT_YMD
FROM APPOINTMENT AS A INNER JOIN PATIENT AS P USING(PT_NO)
    INNER JOIN DOCTOR AS D ON A.MDDR_ID = D.DR_ID
WHERE A.APNT_YMD REGEXP '2022-04-13'
    AND A.APNT_CNCL_YN = 'N'
        AND A.MCDP_CD = 'CS'
ORDER BY A.APNT_YMD ASC;
```
