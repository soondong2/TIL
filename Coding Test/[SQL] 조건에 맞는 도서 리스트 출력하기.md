# Today I Learned - 2023/01/10 Tue

# 조건에 맞는 도서 리스트 출력하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/144853
- 난이도 : Level1

## 풀이
```sql
SELECT
    book_id,
    DATE_FORMAT(published_date, '%Y-%m-%d') AS published_date
FROM BOOK
WHERE published_date REGEXP '2021' AND category = '인문'
ORDER BY PUBLISHED_DATE ASC
```
