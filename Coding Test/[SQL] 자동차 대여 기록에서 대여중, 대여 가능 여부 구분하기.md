# Today I Learned - 2023/02/12 Sun

# 자동차 대여 기록에서 대여중 / 대여 가능 여부 구분하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/157340
- 난이도 : Level3

## 풀이
```sql
SELECT
    car_id,
    (CASE
        WHEN car_id IN (SELECT car_id
                        FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
                        WHERE '2022-10-16'  BETWEEN DATE_FORMAT(start_date, '%Y-%m-%d')
                            AND DATE_FORMAT(end_date, '%Y-%m-%d')) THEN '대여중'
        ELSE '대여 가능'
    END) AS 'availbility'
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
GROUP BY 1
ORDER BY 1 DESC;
```
