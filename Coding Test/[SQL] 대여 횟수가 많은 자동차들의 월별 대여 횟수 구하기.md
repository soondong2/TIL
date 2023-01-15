# Today I Learned - 2023/01/15 Sun

# 대여 횟수가 많은 자동차들의 월별 대여 횟수 구하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/151139
- 난이도 : Level3

## 풀이
```sql
SELECT MONTH(start_date) AS month, car_id, COUNT(*) AS records
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
WHERE car_id IN (SELECT car_id
                 FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
                 WHERE start_date BETWEEN '2022-08-01' AND '2022-10-31'
                 GROUP BY car_id
                 HAVING COUNT(*) >= 5)
    AND start_date BETWEEN '2022-08-01' AND '2022-10-31'
GROUP BY MONTH(start_date), car_id
ORDER BY month ASC, car_id DESC;
```
