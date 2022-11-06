# Today I Learned - 2022/11/07 Mon

# 카테고리 별 상품 개수 구하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/131529
- 난이도 : Level2
<br>

## 풀이
```sql
SELECT
    SUBSTRING(PRODUCT_CODE, 1, 2) AS CATEGORY,
    COUNT(*) AS PRODUCTS
FROM PRODUCT
GROUP BY SUBSTRING(PRODUCT_CODE, 1, 2)
ORDER BY CATEGORY ASC
```
