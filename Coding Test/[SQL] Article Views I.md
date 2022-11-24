# Today I Learned - 2022/11/24 Thur

# Article Views I
- 출처 : https://leetcode.com/problems/article-views-i/description/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT DISTINCT(author_id) AS id
FROM Views
WHERE author_id = viewer_id
ORDER BY author_id ASC
```
