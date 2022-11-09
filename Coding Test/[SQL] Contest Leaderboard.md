# Today I Learned - 2022/11/09 Wed

# Contest Leaderboard
- 출처 : https://www.hackerrank.com/challenges/contest-leaderboard/problem?isFullScreen=true
- 난이도 : Intermediate(Medium)
<br>

## 풀이
```sql
SELECT
    H.hacker_id,
    H.name,
    SUM(sub.max_score) AS score
FROM (SELECT hacker_id, MAX(score) AS max_score
      FROM Submissions
      GROUP BY hacker_id, challenge_id) AS sub
      INNER JOIN Hackers AS H ON sub.hacker_id = H.hacker_id
GROUP BY H.hacker_id, H.name
HAVING score != 0
ORDER BY score DESC, H.hacker_id ASC;
```
<br>

- hacker_id와 challenge_id를 GROUP BY한 뒤 같은 challenge_id가 두 개 이상일 경우 MAX(score)를 통해 최대 점수만 가져온다.
- 위의 내용을 서브쿼리로 만든 후 Hackers 테이블과 JOIN한다.
- hacker_id와 name이 필요하기 때문에 GROUP BY를 해준다.
- score가 0점인 해커는 제외시키기 위해 HAVING 절에 조건을 추가 해준다.
- 마지막 정렬 조건을 만족하면 완료된다.
