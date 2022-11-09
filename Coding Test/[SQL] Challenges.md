# Today I Learned - 2022/11/09 Wed

# Challenges
- 출처 : https://www.hackerrank.com/challenges/challenges/problem?isFullScreen=true
- 난이도 : Intermediate(Medium)
<br>

## 풀이
```sql
SELECT H.hacker_id, H.name, COUNT(*) AS challenges_created
FROM Hackers AS H INNER JOIN Challenges AS C ON H.hacker_id = C.hacker_id
GROUP BY H.hacker_id, H.name
HAVING challenges_created IN (SELECT sub1.challenges_created
                              FROM(SELECT hacker_id, COUNT(*) AS challenges_created
                                   FROM challenges
                                   GROUP BY hacker_id) AS sub1
                              GROUP BY sub1.challenges_created
                              HAVING COUNT(*) = 1)
    OR challenges_created = (SELECT MAX(challenges_created)
                             FROM(SELECT COUNT(*) AS challenges_created
                                  FROM challenges
                                  GROUP BY hacker_id) AS sub2)
ORDER BY challenges_created DESC, H.hacker_id ASC;
```
<br>

- hacker_id, 이름 및 각 학생이 만든 총 과제 수를 인쇄하는 쿼리를 작성하시오.
- 총 과제 수를 기준으로 결과를 내림차순으로 정렬합니다.
- 두 명 이상의 학생이 동일한 수의 문제를 만든 경우 hacker_id별로 결과를 정렬합니다. 
- 두 명 이상의 학생이 동일한 수의 문제를 생성했거나 해당 카운트가 최대 문제 수보다 작으면 해당 학생을 결과에서 제외합니다.

맨 아래 조건이 포인트이다.
- 두 명 이상의 학생이 동일한 수의 문제를 생성한 경우 결과에서 제외 -> hacker_id로 GROUP BY하고 COUNT한 값이 1개(고유값)이어야 한다.
- 고유값이 아닌 경우는 최대 문제 수와 같을 때 출력 시킨다. -> GROUP BY를 통해 COUNT 값을 구하고 그 값의 MAX 값을 구한다.
- HAVING 절에 서브쿼리로 작성해야 하며 OR로 연결시켜준다.
