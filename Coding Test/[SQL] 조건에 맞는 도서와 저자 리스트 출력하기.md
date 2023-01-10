# Today I Learned - 2023/01/10 Tue

# 조건에 맞는 도서와 저자 리스트 출력하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/144854
- 난이도 : Level2
<br>

## 풀이
```sql
SELECT
    B.book_id,
    A.author_name,
    DATE_FORMAT(B.published_date, '%Y-%m-%d') AS published_date 
FROM BOOK AS B INNER JOIN AUTHOR AS A
    ON B.author_id = A.author_id
WHERE B.category = '경제'
ORDER BY published_date ASC;
```
