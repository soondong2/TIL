# Today I Learned - 2022/11/23 Wed

# Swap Salary
- 출처 : https://leetcode.com/problems/swap-salary/
- 난이도 : Easy
<br>

## 풀이
```sql
UPDATE Salary
SET sex = (CASE
            WHEN sex = 'f' THEN 'm'
            ELSE 'f'
           END)
```
