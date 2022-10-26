# Today I Learned - 2022/10/26 Wed

# 가격대 별 상품 개수 구하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/131530
- 난이도 : Level2
<br>

## 풀이
```sql
SELECT
    TRUNCATE(PRICE, -4) AS PRICE,
    COUNT(*) AS PRODUCTS
FROM PRODUCT
GROUP BY TRUNCATE(PRICE, -4)
ORDER BY PRICE ASC;
```

### TRUNCATE
- 만약 PRICE가 72000라면 70000으로 됨
```sql
TRUNCATE(PRICE, -4)
```
