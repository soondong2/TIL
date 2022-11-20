# Today I Learned - 2022/11/20 Sun

# Find Customer Referee
- 출처 : https://leetcode.com/problems/find-customer-referee/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT name
FROM Customer
WHERE referee_id != 2 OR referee_id IS NULL
```
