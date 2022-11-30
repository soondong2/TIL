# Today I Learned - 2022/11/30 Wed

# Group Sold Products By The Date
- 출처 : https://leetcode.com/problems/group-sold-products-by-the-date/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT
    sell_date,
    COUNT(DISTINCT(product)) AS num_sold,
    GROUP_CONCAT(DISTINCT(product) ORDER BY product ASC) AS products
FROM Activities
GROUP BY sell_date
```
