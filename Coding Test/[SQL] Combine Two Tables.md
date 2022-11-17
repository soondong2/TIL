# Today I Learned - 2022/11/17 Thur

# Combine Two Tables
- 출처 : https://leetcode.com/problems/combine-two-tables/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT P.firstName, P.lastName, A.city, A.state 
FROM Person AS P LEFT OUTER JOIN Address AS A ON P.personID = A.personID;
```
