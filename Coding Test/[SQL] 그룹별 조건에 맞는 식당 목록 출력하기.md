# Today I Learned - 2022/11/06 Sun

# 그룹별 조건에 맞는 식당 목록 출력하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/131124
- 난이도 : Levvel4
<br>

## 풀이
```sql
SELECT
    P.MEMBER_NAME,
    R.REVIEW_TEXT,
    DATE_FORMAT(R.REVIEW_DATE, '%Y-%m-%d') AS REVIEW_DATE
FROM MEMBER_PROFILE AS P INNER JOIN REST_REVIEW AS R
    USING(MEMBER_ID)
WHERE P.MEMBER_ID IN
    (SELECT P.MEMBER_ID
    FROM MEMBER_PROFILE AS P INNER JOIN REST_REVIEW AS R
        USING(MEMBER_ID)
    GROUP BY P.MEMBER_ID
    HAVING COUNT(*) = (SELECT COUNT(REVIEW_TEXT) AS 'NUM'
                       FROM REST_REVIEW
                       GROUP BY MEMBER_ID
                       ORDER BY NUM DESC
                       LIMIT 1))
ORDER BY R.REVIEW_DATE ASC, R.REVIEW_TEXT ASC;
```
