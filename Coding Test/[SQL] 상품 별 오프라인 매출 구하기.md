# Today I Learned - 2022/11/06 Sun

# 상품 별 오프라인 매출 구하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/131533
- 난이도 : Level3
<br>

## 풀이
```sql
SELECT
    P.PRODUCT_CODE,
    (SUM(SALES_AMOUNT) * PRICE) AS SALES
FROM PRODUCT AS P INNER JOIN OFFLINE_SALE AS S
    USING(PRODUCT_ID)
GROUP BY P.PRODUCT_CODE
ORDER BY SALES DESC, P.PRODUCT_CODE ASC
```
