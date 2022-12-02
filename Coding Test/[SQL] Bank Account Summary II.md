# Today I Learned - 2022/12/02 Fri

# Bank Account Summary II
- 출처 : https://leetcode.com/problems/bank-account-summary-ii/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT U.name, SUM(T.amount) AS balance
FROM Users AS U INNER JOIN Transactions AS T ON U.account = T.account
GROUP BY U.name
HAVING balance > 10000
ORDER BY balance DESC;
```
