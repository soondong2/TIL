# Today I Learned - 2023/02/15 Wed

# 특정 기간동안 대여 가능한 자동차들의 대여비용 구하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/157339#qna
- 난이도 : Level4

## 풀이
```sql
WITH subtable AS(
SELECT A.car_id, A.car_type, A.daily_fee, C.discount_rate
FROM (
    SELECT car_id, car_type, daily_fee
    FROM car_rental_company_car
    WHERE car_id NOT IN (SELECT car_id
                         FROM car_rental_company_rental_history
                         WHERE start_date >= '2022-11-01'
                            OR end_date >= '2022-11-01')) AS A
    INNER JOIN car_rental_company_rental_history AS B ON A.car_id = B.car_id 
    INNER JOIN car_rental_company_discount_plan AS C ON A.car_type = C.car_type
WHERE A.car_type IN ('세단', 'SUV')
    AND C.duration_type = '30일 이상'
GROUP BY 1, 2, 3, 4
)

SELECT 
    car_id,
    car_type,
    ROUND(daily_fee * (1 - (discount_rate * 0.01)) * 30) AS fee
FROM subtable
WHERE ROUND(daily_fee * (1 - (discount_rate * 0.01)) * 30) BETWEEN 500000 AND 1999999
ORDER BY 3 DESC, 2 ASC, 1 DESC;
```
