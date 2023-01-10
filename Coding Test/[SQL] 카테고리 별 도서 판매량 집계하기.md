# Today I Learned - 2023/01/10 Tue
# 카테고리 별 도서 판매량 집계하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/144855
- 난이도 : Level3

## 풀이
```sql
SELECT A.category, SUM(B.sales) AS total_sales
FROM BOOK AS A INNER JOIN BOOK_SALES AS B
    ON A.book_id = B.book_id
WHERE B.sales_date REGEXP '2022-01'
GROUP BY A.category
ORDER BY A.category ASC;
```
