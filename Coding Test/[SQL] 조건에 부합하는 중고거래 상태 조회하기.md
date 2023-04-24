# Today I Learned - 2023/04/24

# 조건에 부합하는 중고거래 상태 조회하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/164672
- 난이도 : Level2

## 풀이
```sql
SELECT
    board_id,
    writer_id,
    title,
    price,
    (CASE
     WHEN status = 'SALE' THEN '판매중'
     WHEN status = 'RESERVED' THEN '예약중'
     ELSE '거래완료'
    END)AS status
FROM used_goods_board
WHERE DATE_FORMAT(created_date, '%Y-%m-%d') = '2022-10-05'
ORDER BY board_id DESC;
```
