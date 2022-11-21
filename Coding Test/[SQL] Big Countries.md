# Today I Learned - 2022/11/21 Mon

# Big Countries
- 출처 : https://leetcode.com/problems/big-countries/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT name, population, area
FROM World
WHERE area >= 3000000 OR population >= 25000000
```
