# Today I Learned - 2022/12/08 Thur

# Rank Scores
- 출처 : https://leetcode.com/problems/rank-scores/
- 난이도 : Medium
<br>

## 풀이
```sql
SELECT
    score,
    DENSE_RANK() OVER(ORDER BY score DESC) AS 'rank'
FROM Scores;
```
<br>

## 정리
- `RANK() OVER(ORDER BY 컬럼 정렬기준)` : 동등한 순위가 있을 경우, 건너 뛰고 다음 등수가 나타난다.
  ex) 1, 2, 3, 3, 5
- `DENSE_RANK() OVER(ORDER BY 컬럼 정렬기준)` : 동등한 순위가 있더라도 건너 뛰지 않는다.
  ex) 1, 2, 3, 3, 4
