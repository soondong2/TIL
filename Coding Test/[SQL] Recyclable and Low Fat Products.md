# Today I Learned - 2022/12/04 Sun

# Recyclable and Low Fat Products
- 출처 : https://leetcode.com/problems/recyclable-and-low-fat-products/
- 난이도 : Easy
<br>

## 풀이 
```sql
SELECT product_id
FROM Products
WHERE low_fats = 'Y' AND recyclable = 'Y';
```
