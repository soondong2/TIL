# Today I Learned - 2022/12/20 Wed

# WITH RECURSIVE
- WITH 구문은 메모리 상에 가상의 테이블을 저장할 때 사용된다.\
- `RECURSIVE`의 여부에 따라 `재귀`, `비재귀` 두 가지 방법으로 사용 가능하다.
```sql
WITH [RECURSIVE] TABLE명 AS (
    SELECT  # 비반복문. 무조건 필수
    [UNION ALL]  # RECURSIVE 사용 시 필수. 다음에 이어붙어야 할 때 사용
    SELECT 
    [WHERE]  # RECURSIVE 사용 시 필수. 정지 조건 필요할 때 사용
)
```

<br>

- `WITH` 구문 이후에 오는 쿼리에서 임시 테이블의 테이블명을 사용하여 값을 참조할 수 있다.
```sql
WITH table명 AS(
    SELECT 초기값 AS 별칭
		FROM table명
)
```

```sql
# 사용 예시
WITH TMP AS(
    SELECT id    
           ,num
           ,LAG(num, 1, NULL) OVER(ORDER BY id)AS num2 
           ,LAG(num, 2, NULL) OVER(ORDER BY id)AS num3
    FROM Logs
)

SELECT DISTINCT num AS ConsecutiveNums
FROM TMP 
WHERE num = num2 AND num2 = num3
```
<br>

- `WITH RECURSIVE` 구문은 가상 테이블을 생성하면서 가상 테이블 자신의 값을 참조하여 값을 결정할 때 사용된다.
```sql
WITH RECURSIVE table명 AS(
    SELECT 초기값 AS 별칭
		UNION ALL
		SELECT 별칭별 계산식 FROM table명
		WHERE 조건
)
```

```sql
# 사용 예시
# 1 ~ 10까지의 수를 갖는 테이블 생성
WITH RECURSIVE number AS(
		SELECT 1 AS num
		UNION ALL
		SELECT num + 1 FROM number
		WHERE num < 10
)
# 출력 1, 2, 3, 4, 5, 6, 7. 8. 9. 10
```
