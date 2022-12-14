# Today I Learned - 2022/12/14 Wed

# Consecutive Numbers
- 출처 : https://leetcode.com/problems/consecutive-numbers/
- 난이도 : Medium
<br>

## 풀이
```sql
SELECT DISTINCT(num1) AS ConsecutiveNums
FROM
    (SELECT
        num AS num1,
        LEAD(num) OVER(ORDER BY id) AS num2,
        LEAD(num, 2) OVER(ORDER BY id) AS num3
    FROM Logs) AS sub
WHERE num1 = num2 AND num2 = num3
```
