# Today I Learned - 2022/11/05 Sun

# 식품분류별 가장 비싼 식품의 정보 조회하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/131116
- 난이도 : Level4
<br>

## 풀이
```sql
SELECT
    A.CATEGORY, 
    A.MAX_PRICE,
    B.PRODUCT_NAME
FROM (SELECT CATEGORY, MAX(PRICE) AS MAX_PRICE
      FROM FOOD_PRODUCT
      WHERE CATEGORY IN ('과자', '국', '김치', '식용유')
      GROUP BY CATEGORY) AS A
    INNER JOIN (SELECT * FROM FOOD_PRODUCT) AS B
        ON A.CATEGORY = B.CATEGORY AND A.MAX_PRICE = B.PRICE
ORDER BY A.MAX_PRICE DESC;
```
