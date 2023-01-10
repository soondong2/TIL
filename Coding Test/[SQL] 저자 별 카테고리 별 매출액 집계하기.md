# Today I Learned - 2023/01/10 Tue

# 저자 별 카테고리 별 매출액 집계하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/144856
- 난이도 : Level4

## 풀이
```sql
SELECT
    A.author_id,
    B.author_name,
    A.category,
    SUM(A.price * C.sales) AS total_sales
FROM book AS A
    INNER JOIN author AS B ON A.author_id = B.author_id
    INNER JOIN book_sales AS C ON A.book_id = C.book_id
WHERE C.sales_date REGEXP '2022-01'
GROUP BY author_id, author_name, category
ORDER BY author_id ASC, category DESC;
```
