# Today I Learned - 2022/10/25 Tue

# 가격이 제일 비싼 식품의 정보 출력하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/131115
- 난이도 : Level2
<br>

## 풀이
```sql
SELECT *
FROM FOOD_PRODUCT
WHERE PRICE = (SELECT MAX(PRICE) FROM FOOD_PRODUCT);
```
