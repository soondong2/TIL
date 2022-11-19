# Today I Learned - 2022/11/19 Sat

# Game Play Analysis I
- 출처 : https://leetcode.com/problems/game-play-analysis-i/
- 난이도 : 
<br>

## 풀이
```sql
SELECT player_id, MIN(event_date) AS first_login
FROM Activity
GROUP BY player_id
```
