# Today I Learned - 2023/01/08 Sun

# DISTINCT
SELECT 시 DISTINCT를 사용하면 중복 값을 제외한 결과 값이 출력된다. 즉, 같은 결과의 행이라면 **중복을 제거**할 수 있다.

<br>

## 단일 컬럼
```sql
SELECT DISTINCT 컬럼
FROM table명
```

<br>

## 다중 컬럼
컬럼1 + 컬럼2의 중복되는 값이 존재한다면, 중복되는 row가 제거되어 조회된다.
```sql
SELECT DISTINCT 컬럼1, 컬럼2
FROM table명
```

<br>

## DISTINCT ON
- 어떤 컬럼에 대해 중복을 제거할지 명시가 가능한 문법이다.
- `DISTINCT ON()`은 PostgreSQL에만 존재하는 고유 문법이다.
- ON 안에 작성한 컬럼 값을 기준으로 중복 제거 후 조회된다.
- **DISTINCT ON 절의 컬럼과 ORDER BY 절에서 첫 번째 컬럼이 일치**해야 한다.
```sql
SELECT DISTINCT ON(컬림1), 컬럼2
FROM table명
ORDER BY 컬럼1, 컬럼2
```
