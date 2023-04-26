# Today I Learned - 2023-04-26

# 조회수가 가장 많은 중고거래 게시판의 첨부파일 조회하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/164671
- 난이도 : Level3

## 풀이
```sql
-- /home/grep/src/board_id/file_id+file_name+file_ext

WITH temp AS (
SELECT * 
FROM used_goods_file
WHERE board_id = (SELECT board_id
                  FROM used_goods_board
                  WHERE views = (SELECT MAX(views) AS max_view FROM used_goods_board))
)
SELECT CONCAT('/home/grep/src/', board_id, '/', file_id, file_name, file_ext) AS file_path
FROM temp
ORDER BY file_id DESC;
```
