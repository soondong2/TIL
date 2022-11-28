# Today I Learned - 2022/11/28 Mon

# Reformat Department Table
- 출처 : https://leetcode.com/problems/classes-more-than-5-students/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT class
FROM Courses
GROUP BY class
HAVING COUNT(*) >= 5
```
