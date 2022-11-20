# Today I Learned - 2022/11/20 Sun

# Customer Placing the Largest Number of Orders
- 출처 : https://leetcode.com/problems/customer-placing-the-largest-number-of-orders/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT customer_number
FROM Orders
GROUP BY customer_number
ORDER BY COUNT(*) DESC
LIMIT 1;
```
