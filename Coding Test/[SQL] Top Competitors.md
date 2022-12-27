# Today I Learned - 2022/11/09 Wed

# Top Competitors
- 출처 : https://www.hackerrank.com/challenges/full-score/problem?isFullScreen=true
- 난이도 : Intermediate(Medium)
<br>

## 풀이
```sql
SELECT H.hacker_id, H.name
FROM Submissions AS S
    INNER JOIN Hackers AS H ON S.hacker_id = H.hacker_id
    INNER JOIN Challenges AS C ON S.challenge_id = C.challenge_id
    INNER JOIN Difficulty AS D ON C.difficulty_level = D.difficulty_level
WHERE D.score = S.score
GROUP BY H.hacker_id, H.name
HAVING COUNT(H.hacker_id) > 1
ORDER BY COUNT(H.hacker_id) DESC, H.hacker_id ASC;
```
<br>

- 테이블들을 `JOIN` 해준다.
- `Difficulty` 테이블에 해당 등급의 만점 Score가 나타나져있다.
- `Submissions` 테이블에서 해당 등급에 Challenge에 따른 Score가 입력되어 있다.
- 만점을 받은 hacker_id가 2개 이상인 경우를 찾아서 조회한다.
