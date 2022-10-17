# Today I Learned - 2022/10/17 Mon

# 재구매가 일어난 상품과 회원 리스트 구하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/131536
- 난이도 : Level2
<br>

## 풀이
```sql
SELECT USER_ID, PRODUCT_ID
FROM ONLINE_SALE
GROUP BY USER_ID, PRODUCT_ID
HAVING COUNT(PRODUCT_ID) > 1
ORDER BY USER_ID ASC, PRODUCT_ID DESC;
```
