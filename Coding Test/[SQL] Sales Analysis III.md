# Today I Learned - 2022/11/29 Tue

# Sales Analysis III
- 출처 : https://leetcode.com/problems/sales-analysis-iii/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT product_id, product_name
FROM product
WHERE product_id NOT IN (SELECT P.product_id
                         FROM Product AS P LEFT OUTER JOIN Sales AS S ON P.product_id = S.product_id
                         WHERE sale_date NOT BETWEEN '2019-01-01' AND '2019-03-31'
                          OR S.product_id IS NULL)

```
