# Today I Learned - 2022/12/03 Sat

# Find Followers Count
- 출처 : https://leetcode.com/problems/find-followers-count/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT user_id, COUNT(DISTINCT(follower_id)) AS followers_count
FROM Followers
GROUP BY user_id
ORDER BY user_id ASC;
```
