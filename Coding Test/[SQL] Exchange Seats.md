# Today I Laerned - 2022/12/17 Sat

# Exchange Seats
- 출처 : https://leetcode.com/problems/exchange-seats/
- 난이도 : Medium
<br>

## 풀이
```sql
SELECT
    T1.id,
    (CASE
        WHEN T1.p_id IS NULL THEN 'Root'
        WHEN T2.id IS NOT NULL THEN 'Inner'
        ELSE 'Leaf'
    END) AS type
FROM Tree AS T1 LEFT OUTER JOIN Tree AS T2 ON T1.id = T2.p_id
GROUP BY T1.id;
```
```sql
SELECT
    id,
    (CASE
        WHEN p_id IS NULL THEN 'Root'
        WHEN id NOT IN (SELECT p_id FROM Tree WHERE p_id IS NOT NULL) THEN 'Leaf' 'Leaf'
        ELSE 'Inner'
    END) AS type
FROM Tree;
```
