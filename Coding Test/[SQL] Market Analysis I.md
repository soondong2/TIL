# Today I Learned - 2022/12/18 Sun

# Market Analysis I
- 출처 : https://leetcode.com/problems/market-analysis-i/
- 난이도 : Medium
<br>

## 풀이
```sql
SELECT
    U.user_id AS buyer_id,
    U.join_date,
    IFNULL(COUNT(O.order_date), 0) AS orders_in_2019
FROM Users AS U LEFT OUTER JOIN Orders AS O ON U.user_id = O.buyer_id
    AND YEAR(O.order_date) = '2019'
GROUP BY U.user_id
```
