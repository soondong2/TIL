# Today I Learned - 2022/12/05 Mon

# Rearrange Products Table
- 출처 : https://leetcode.com/problems/rearrange-products-table/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT *
FROM(
    (SELECT product_id, 'store1' AS store, store1 AS price
    FROM Products)
    UNION ALL
    (SELECT product_id, 'store2' AS store, store2 AS price
    FROM Products)
    UNION ALL
    (SELECT product_id, 'store3' AS store, store3 AS price
    FROM Products)) AS result
WHERE price IS NOT NULL
```
