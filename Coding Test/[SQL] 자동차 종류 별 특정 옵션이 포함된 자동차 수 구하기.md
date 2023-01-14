# Today I Learned - 2023/01/14 Sat

# 자동차 종류 별 특정 옵션이 포함된 자동차 수 구하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/151137
- 난이도 : Level2

## 풀이
```sql
SELECT car_type, COUNT(*) AS cars
FROM CAR_RENTAL_COMPANY_CAR
WHERE options REGEXP '통풍시트'
    OR options REGEXP '열선시트'
    OR options REGEXP '가죽시트'
GROUP BY car_type
ORDER BY car_type ASC;
```
