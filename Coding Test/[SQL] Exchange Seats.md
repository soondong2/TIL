# Today I Learned - 2022/12/19 Mon

# Exchange Seats
- 출처 : https://leetcode.com/problems/exchange-seats/description/
- 난이도 : Medium
<br>

## 풀이
```sql
SELECT id, IF(student2 IS NULL, student1, student2) AS student
FROM
  (SELECT
      id, student AS student1,
      (CASE
          WHEN MOD(id, 2) != 0 THEN LEAD(student) OVER()
          ELSE LAG(student) OVER()
      END) AS student2
FROM Seat) AS sub
```
Runtime
270 ms
