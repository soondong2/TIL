# Today I Learned - 2022/11/22 Tue

# Delete Duplicate Emails
- 출처 : https://leetcode.com/problems/delete-duplicate-emails/
- 난이도 : Easy
<br>

## 풀이1
```sql
DELETE
FROM Person
WHERE id NOT IN (SELECT sub.min_id
                 FROM (SELECT email, MIN(id) AS min_id FROM Person GROUP BY email) sub)
```
## 풀이2
```sql
DELETE p1
FROM Person AS p1 INNER JOIN Person AS p2 ON p1.email = p2.email
WHERE p1.id > p2.id
```
