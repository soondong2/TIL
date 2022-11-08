# Today I Learned - 2022/11/08 Tue

# Binary Tree Nodes
- 출처 : https://www.hackerrank.com/challenges/binary-search-tree-1/problem?isFullScreen=true
- 난이도 : Intermediate(Medium)
<br>

## 풀이
### SELF JOIN
```sql
SELECT
    DISTINCT(B1.N),
    (CASE
        WHEN B1.P IS NULL THEN 'Root'
        WHEN B2.N IS NULL THEN 'Leaf'
        ELSE 'Inner'
    END) 
FROM BST AS B1 LEFT OUTER JOIN BST AS B2
    ON B1.N = B2.P
ORDER BY B1.N ASC;
```

### JOIN 사용하지 않음
```sql
SELECT
    DISTINCT(N),
    (CASE
        WHEN P IS NULL THEN 'Root'
        WHEN N IN (SELECT P FROM BST) THEN 'Inner'
        ELSE 'Leaf'
    END) 
FROM BST
ORDER BY N ASC;
```
