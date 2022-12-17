# Today I Learnend - 2022/12/17 Sat

# Capital Gain/Loss
- 출처 : https://leetcode.com/problems/capital-gainloss/description/
- 난이도 : Medium
<br>

## 풀이
- JOIN 사용
```sql
SELECT
    A.stock_name,
    (B.Sell - A.Buy) AS capital_gain_loss
FROM
    (SELECT stock_name, SUM(price) AS buy
    FROM Stocks
    WHERE operation = 'Buy'
    GROUP BY stock_name) AS A
    INNER JOIN 
    (SELECT stock_name, SUM(price) AS Sell
    FROM Stocks
    WHERE operation = 'Sell'
    GROUP BY stock_name) AS B
    ON A.stock_name = B.stock_name
```
- WITH 사용 -> 훨씬 더 효율적인 코드
```sql
WITH result AS (
    SELECT
        stock_name,
        (CASE
            WHEN operation = 'Buy' THEN (price * -1)
            ELSE price
        END) AS new_price
    FROM Stocks
)

SELECT stock_name, SUM(new_price) AS capital_gain_loss
FROM result
GROUP BY stock_name
```
