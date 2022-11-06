# Today I Learned - 2022/11/05 Sat

# 과일로 만든 아이스크림 고르기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/133025
- 난이도 : Level1
<br>

## 풀이
```sql
SELECT F.FLAVOR 
FROM FIRST_HALF AS F INNER JOIN ICECREAM_INFO AS I
    ON F.FLAVOR = I.FLAVOR
WHERE F.TOTAL_ORDER >= 3000 AND I.INGREDIENT_TYPE = 'fruit_based'
ORDER BY F.TOTAL_ORDER DESC;
```
