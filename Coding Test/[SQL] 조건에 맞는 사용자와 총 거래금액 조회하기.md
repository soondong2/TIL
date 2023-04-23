# Today I Learned - 2023/04/23 

# 조건에 맞는 사용자와 총 거래금액 조회하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/164668
- 난이도 : Level3

## 풀이
```sql
SELECT
    A.writer_id,
    B.nickname,
    SUM(A.price) AS total_sales
FROM used_goods_board AS A INNER JOIN used_goods_user AS B ON A.writer_id = B.user_id
WHERE A.status = 'DONE'
GROUP BY A.writer_id
HAVING total_sales >= 700000
ORDER BY total_sales ASC;
```
