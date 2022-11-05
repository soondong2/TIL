# Today I Learned - 2022/11/05 Sum

# 즐겨찾기가 가장 많은 식당 정보 출력하기
- 출처 : 
- 난이도 : Level3
<br>

## 풀이
```sql
SELECT 
    FOOD_TYPE, 
    REST_ID,
    REST_NAME,
    FAVORITES
FROM REST_INFO
WHERE (FOOD_TYPE, FAVORITES) IN (SELECT FOOD_TYPE, MAX(FAVORITES)
                                 FROM REST_INFO
                                 GROUP BY FOOD_TYPE)
ORDER BY FOOD_TYPE DESC;
```
위 방법으로도 같은 결과값이 나오고 정답으로 인정되지만, 정석은 아래와 같이 풀어야 함 -> `INNER JOIN` 사용

```sql
SELECT 
    A.FOOD_TYPE, 
    B.REST_ID,
    B.REST_NAME,
    A.FAVORITES
FROM (SELECT FOOD_TYPE, MAX(FAVORITES) AS FAVORITES
      FROM REST_INFO
      GROUP BY FOOD_TYPE) AS A
    INNER JOIN (SELECT * FROM REST_INFO) AS B
        ON A.FOOD_TYPE = B.FOOD_TYPE AND A.FAVORITES = B.FAVORITES
ORDER BY A.FOOD_TYPE DESC;
```
