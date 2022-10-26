# Today I Learned - 2022/10/26 Wed

# 입양 시각 구하기(2)
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/59413
- 난이도 : Level4
<br>

## 풀이
```sql
SET @HOUR := -1; 
SELECT
    (@HOUR := @HOUR + 1) AS HOUR,
    (SELECT COUNT(*) FROM ANIMAL_OUTS WHERE @HOUR = HOUR(DATETIME)) AS COUNT
FROM ANIMAL_OUTS
WHERE @HOUR < 23
ORDER BY HOUR ASC;
```
<br>

## 정리
### 변수 생성
```sql
SET @변수명 := 초기값;
```

### 변수 사용
- 초기값 -1에서부터 각 행마다 @HOUR를 1씩 증가 -> 0, 1, 2, 3, ...
```sql
SET @HOUR := -1;
SELECT (@HOUR := @HOUR + 1) AS HOUR
```
- 초기값 -1에서 모든 @HOUR를 +1 증가 -> 0, 0, 0, 0, ...
```sql
SET @HOUR := -1;
SELECT (@HOUR = @HOUR + 1) AS HOUR
```

