# Today I Learned - 2022/11/07 Mon

# 상품을 구매한 회원 비율 구하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/131534
- 난이도 : Level5
<br>

## 풀이
```sql
SELECT
    YEAR(O.SALES_DATE) AS YEAR,
    MONTH(O.SALES_DATE) AS MONTH,
    COUNT(DISTINCT(U.USER_ID)) AS PUCHASSED_USERS,
    ROUND((COUNT(DISTINCT(U.USER_ID)) / (SELECT COUNT(*)
                                         FROM USER_INFO
                                         WHERE YEAR(JOINED) = '2021')), 1) AS PUCHASED_RATIO
FROM USER_INFO AS U INNER JOIN ONLINE_SALE AS O USING(USER_ID)
WHERE YEAR(U.JOINED) = '2021' 
GROUP BY YEAR(O.SALES_DATE), MONTH(O.SALES_DATE)
ORDER BY YEAR ASC, MONTH ASC;
```
