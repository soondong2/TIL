# Today I Learned - 2022/11/18 Fri

# Customers Who Never Order
- 출처 : https://leetcode.com/problems/customers-who-never-order/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT C.name AS Customers
FROM Customers AS C LEFT OUTER JOIN Orders AS O ON C.id = O.customerId
WHERE O.customerId IS NULL
```
