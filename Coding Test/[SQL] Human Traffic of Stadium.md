# Today I Learned - 2023/01/08 Sun

# Human Traffic of Stadium
- 출처 : https://leetcode.com/problems/human-traffic-of-stadium/
- 난이도 : Hard
<br>

## 풀이
```sql
-- id - ROW_NUMBER() 해주면 연속적인 id에 대해서 같은 값이 나타나게 되는 것을 이용한다.
WITH subtable AS(
    SELECT 
        id,
        visit_date,
        people,
        id-ROW_NUMBER() OVER(ORDER BY id ASC) AS value
    FROM Stadium
    WHERE people >= 100
    )

SELECT id, visit_date, people
FROM subtable
WHERE value IN (SELECT value FROM subtable GROUP BY value HAVING COUNT(*) >= 3)
```
