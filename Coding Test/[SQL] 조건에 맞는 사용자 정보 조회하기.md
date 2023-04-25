# Today I Learned - 2024/04/25

# 조건에 맞는 사용자 정보 조회하기

- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/164670
- 난이도 : Level3
<br>

## 풀이
```sql
-- JOIN을 사용하지 않고 WHERE절에 서브쿼리 사용
SELECT
    user_id,
    nickname,
    CONCAT(city, ' ', street_address1, ' ', street_address2) AS '전체주소',
    CONCAT(LEFT(TLNO, 3), '-', SUBSTRING(TLNO, 4, 4), '-', RIGHT(TLNO, 4)) AS '전화번호'
FROM used_goods_user
WHERE user_id IN (SELECT writer_id
                  FROM used_goods_board
                  GROUP BY writer_id
                  HAVING COUNT(writer_id) >= 3)
ORDER BY user_id DESC;
```
```sql
-- JOIN 사용
SELECT
    B.user_id,
    B.nickname,
    CONCAT(city, ' ', street_address1, ' ', street_address2) AS '전체주소',
    CONCAT(LEFT(TLNO, 3), '-', SUBSTRING(TLNO, 4, 4), '-', RIGHT(TLNO, 4)) AS '전화번호'
FROM used_goods_board AS A INNER JOIN used_goods_user AS B ON A.writer_id = B.user_id
GROUP BY A.writer_id
HAVING COUNT(A.writer_id) >= 3
ORDER BY A.writer_id DESC;
```
