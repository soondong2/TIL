# Today I Learned - 2022/11/22 Tue

# Not Boring Movies
- 출처 : https://leetcode.com/problems/not-boring-movies/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT * 
FROM Cinema
WHERE id % 2 = 1 AND description != 'boring'
ORDER BY rating DESC
```
