# Today I Learned - 2022/11/06 Sun

# 5월 식품들의 총매출 조회하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/131117
- 난이도 : Level4
<br>

## 풀이
```sql
SELECT
    P.PRODUCT_ID,
    P.PRODUCT_NAME,
    (P.PRICE * SUM(O.AMOUNT)) AS TOTAL_SALES
FROM FOOD_PRODUCT AS P INNER JOIN FOOD_ORDER AS O
    USING(PRODUCT_ID)
WHERE O.PRODUCE_DATE REGEXP '2022-05'
GROUP BY P.PRODUCT_NAME
ORDER BY TOTAL_SALES DESC, P.PRODUCT_ID ASC;
```
