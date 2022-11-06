# Today I Learned - 2022/11/05 Sat

# 성분으로 구분한 아이스크림 총 주문량
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/133026
- 난이도 : Level2
<br>

## 풀이
```sql
SELECT
    I.INGREDIENT_TYPE,
    SUM(TOTAL_ORDER) AS TOTAL_ORDER
FROM FIRST_HALF AS F INNER JOIN ICECREAM_INFO AS I
    ON F.FLAVOR = I.FLAVOR
GROUP BY I.INGREDIENT_TYPE
ORDER BY TOTAL_ORDER ASC;
```
