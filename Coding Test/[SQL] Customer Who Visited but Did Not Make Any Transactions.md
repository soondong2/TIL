# Today I Learned - 2022/12/01 Thur

# Customer Who Visited but Did Not Make Any Transactions
- 출처 : https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT V.customer_id, COUNT(*) AS count_no_trans
FROM Visits AS V LEFT OUTER JOIN Transactions AS T ON V.visit_id = T.visit_id
WHERE T.visit_id IS NULL
GROUP BY V.customer_id
```
