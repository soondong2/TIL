# Today I Learned - 2023/02/14 Tue

# 대여 기록이 존재하는 자동차 리스트 구하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/157341
- 난이도 : Level3

## 풀이
```sql
SELECT car_id
FROM car_rental_company_rental_history
WHERE car_id IN (SELECT car_id
                FROM car_rental_company_car
                WHERE car_type = '세단')
    AND start_date LIKE '2022-10%'
GROUP BY 1
ORDER BY 1 DESC;
```
