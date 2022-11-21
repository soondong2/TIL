# Today I Learned - 2022/11/21 Mon

# Sales Person
- 출처 : https://leetcode.com/problems/sales-person/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT name
FROM SalesPerson
WHERE name NOT IN (SELECT S.name
                   FROM Orders AS O
                    INNER JOIN Company AS C ON O.com_id = C.com_id
                    INNER JOIN SalesPerson AS S ON O.sales_id = S.sales_id
                    WHERE C.name = 'RED')
```
