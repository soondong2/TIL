# Today I Learned - 2023/02/12 Sun

# 자동차 평균 대여 기간 구하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/157342
- 난이도 : Level2

## 풀이
```sql
SELECT
    car_id,
    ROUND(AVG(DATEDIFF(end_date, start_date) + 1), 1) AS average_duration
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
GROUP BY 1
HAVING AVG(DATEDIFF(end_date, start_date) + 1) >= 7
ORDER BY 2 DESC, 1 DESC;
```
