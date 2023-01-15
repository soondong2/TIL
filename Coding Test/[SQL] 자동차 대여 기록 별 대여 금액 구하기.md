# Today I Learned - 2023/01/15 Sub

# 자동차 대여 기록 별 대여 금액 구하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/151141
- 난이도 : Level4

## 풀이
```sql
SELECT
    C.history_id,
    ROUND(daily_fee * ((100 - IFNULL(discount_rate, 0))/100) * diff) AS fee
FROM(
    SELECT
    A.car_type,
    B.history_id,
    A.daily_fee,
    DATEDIFF(B.end_date, B.start_date) + 1 AS diff,
    (CASE
     WHEN DATEDIFF(end_date, start_date) + 1 >= 90 THEN '90일 이상'
     WHEN DATEDIFF(end_date, start_date) + 1 >= 30 THEN '30일 이상'
     WHEN DATEDIFF(end_date, start_date) + 1 >= 7 THEN '7일 이상'
    END) AS duration_type
FROM CAR_RENTAL_COMPANY_CAR AS A
    INNER JOIN CAR_RENTAL_COMPANY_RENTAL_HISTORY AS B ON A.car_id = B.car_id
WHERE A.car_type = '트럭'
) AS C LEFT OUTER JOIN CAR_RENTAL_COMPANY_DISCOUNT_PLAN AS D
    ON C.car_type = D.car_type AND C.duration_type = D.duration_type
GROUP BY C.history_id
ORDER BY fee DESC, C.history_id DESC;
```
