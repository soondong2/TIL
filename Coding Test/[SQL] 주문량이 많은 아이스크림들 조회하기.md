# Today I Learned - 2022/11/07 Mon

# 주문량이 많은 아이스크림들 조회하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/133027
- 난이도 : Level4
<br>

## 풀이
```sql
SELECT
    F.FLAVOR
FROM FIRST_HALF AS F INNER JOIN
    (SELECT
        SHIPMENT_ID,
        FLAVOR,
        SUM(TOTAL_ORDER) AS TOTAL_ORDER
    FROM JULY
    GROUP BY FLAVOR) AS J
        USING(SHIPMENT_ID)
ORDER BY (F.TOTAL_ORDER + J.TOTAL_ORDER) DESC
LIMIT 3;
```
