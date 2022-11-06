# Today I Learned - 2022/11/05 Sat

# 년, 월, 성별 별 상품 구매 회원 수 구하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/131532
- 난이도 : Level4
<br>

## 풀이
```sql
SELECT
    YEAR(O.SALES_DATE) AS YEAR,
    MONTH(O.SALES_DATE) AS MONTH,
    U.GENDER,
    COUNT(DISTINCT(USER_ID)) AS USERS
FROM USER_INFO AS U INNER JOIN ONLINE_SALE AS O
    USING(USER_ID)
GROUP BY YEAR(O.SALES_DATE), MONTH(O.SALES_DATE), U.GENDER
HAVING U.GENDER IS NOT NULL
ORDER BY YEAR ASC, MONTH ASC, GENDER ASC;
```
- 동일한 날짜, 회원 ID, 상품 ID 조합에 대해서는 하나의 판매 데이터만 존재합니다.
- 위 문구는 `DISTINCT`로 중복을 제거해줘야 한다.
