# Today I Learned - 2022/11/14 Mon

# Ollivander's Inventory
- 출처 : https://www.hackerrank.com/challenges/harry-potter-and-wands/problem?isFullScreen=true
- 난이도 : Intermediate(Medium)
<br>

## 풀이1
```sql
SELECT
    W.id,
    WP.age,
    W.coins_needed,
    W.power
FROM Wands AS W INNER JOIN Wands_Property AS WP
    ON W.code = WP.code
WHERE WP.is_evil = 0
    AND W.coins_needed = (SELECT MIN(W1.coins_needed)
                           FROM Wands AS W1 INNER JOIN Wands_Property AS WP1
                            ON W1.code = WP1.code
                           WHERE WP1.is_evil = 0
                            AND W.power = W1.power
                            AND WP.age = WP1.age)
ORDER BY W.power DESC, WP.age DESC
```
<br>

## 풀이2
```sql
SELECT
    W1.id,
    WP.age,
    W.coins_needed,
    W.power
FROM
    (SELECT code, power, MIN(coins_needed) AS coins_needed
    FROM Wands
    GROUP BY code, power) AS W
    INNER JOIN Wands AS W1
        ON W.code = W1.code
        AND W.power = W1.power
        AND W.coins_needed = W1.coins_needed
    INNER JOIN Wands_Property AS WP ON W.code = WP.code
WHERE WP.is_evil = 0
ORDER BY W.power DESC, WP.age DESC;
```
