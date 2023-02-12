# Today I Learned - 2023/02/12 Sun

# 특정 옵션이 포함된 자동차 리스트 구하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/157343
- 난이도 : Level1

## 풀이
```sql
SELECT *
FROM CAR_RENTAL_COMPANY_CAR
WHERE options LIKE '%네비게이션%'
ORDER BY 1 DESC;
```
