# Today I Learned - 2023/01/13 Fri

# 자동차 대여 기록에서 장기/단기 대여 구분하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/151138
- 난이도 : Level1

## 풀이
```sql
SELECT
    history_id,
    car_id,
    DATE_FORMAT(start_date, '%Y-%m-%d') AS start_date,
    DATE_FORMAT(end_date,'%Y-%m-%d') AS end_date,
    IF(DATEDIFF(end_date, start_date)+1 >= 30, '장기 대여', '단기 대여') AS rent_type
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
WHERE start_date REGEXP '2022-09'
ORDER BY history_id DESC;
```
