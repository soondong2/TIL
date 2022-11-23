# Today I Learned - 2022/11/23 Wed

# Actors and Directors Who Cooperated At Least Three Times
- 출처 : https://leetcode.com/problems/actors-and-directors-who-cooperated-at-least-three-times/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT actor_id, director_id
FROM ActorDirector
GROUP BY actor_id, director_id
HAVING COUNT(*) >= 3;
```
