# Today I Learned - 2022/05/15 Sun

# SQL이란 ❓
`SQL` (Structured Query Language)은 `관계형 데이터베이스` 를 조작하기 위한 언어이다.

<br>

## 📝 SQL문 작성 형식
- 하나의 SQL문 끝에는 `세미콜론(;)`을 작성해줘야 한다. 문법 상 세미콜론이 **하나의 SQL문을 종결하는 단위**이기 때문이다.
- SQL문 안에는 `공백`이나 `개행(줄바꿈)`을 자유롭게 넣을 수 있다.
- MySQL에 기본으로 내장된 키워드를 `예약어`라고 한다. 예약어는 `대문자`로 써주고(가독성을 위해), 나머지 부분은 `소문자`로 작성한다.
- 서로 다른 데이터베이스에 같은 이름의 테이블이 존재할 수 있으므로 `데이터베이스.테이블;`를 사용한다.
- `USE 데이터베이스`는 어떤 데이터베이스를 사용하겠다고 확실하게 정의하는 것이다. 그럼 그 이후로는 `SELECT * FROM 테이블;`로 작성해도 된다.
<br>

## 📝 SQL문 작성 순서
`순서의 법칙`을 지키지 않으면 SQL문을 실행했을 때 에러가 발생한다.

자세한 사항은 [https://dev.mysql.com/doc/refman/8.0/en/select.html](https://dev.mysql.com/doc/refman/8.0/en/select.html) 를 참고하길 바란다.
```sql
SELECT
FROM
WHERE
GROUP BY
HAVING
ORDER BY
```
<br>

## 📝 SQL문 실행 순서
### FROM -> WHERE -> GROUP BY -> SELECT -> HAVING -> ORDER BY
<br>

## SELECT / WHERE
- `SELECT` : 테이블의 데이터를 **조회**할 때 사용하는 구문이다.
- `*` : asterisk, 각 row의 모든 column들의 값을 보여달라는 의미이다.
- `FROM` : '~부터', 어느 테이블에서부터 데이터를 조회할 것인지를 나타낸다.
- FROM 이후에는 데이터를 조회하고 싶은 **테이블의 이름**을 작성한다.
- `WHERE` : 특정 **조건**을 만족하는 row들만 조회한다.
<br>

SELECT
```sql
SELECT * FROM member;
```
```sql
SELECT * FROM member WHERE email = 'abcd@naver.com';
```

WHERE
```sql
SELECT * FROM member WHERE email = 'abcd@naver.com';
```
<br>

```python
USE database;
```

위 코드를 입력해주면 더 이상 `데이터베이스.테이블` 이 아닌 `FROM 테이블` 로 작성하면 된다.
<br>

```sql
SELECT * FROM member WHERE age >= 27;
```

- `BETWEEN A AND B` : A부터 B까지의 구간을 의미한다.
- `NOT BETWEEN A AND B` : A부터 B까지의 구간을 제외하는 것을 의미한다.
```sql
SELECT * FROM .member WHERE age BETWEEN 30 AND 39;
```
```sql
SELECT * FROM member WHERE age NOT BETWEEN 30 AND 39;
```
```sql
SELECT * FROM member WHERE sign_up_day > '2019-01-01';
```

`''` 또는 `""` 안에 들어가는 값은 보통 문자열을 표현할 때 사용한다. 다만 `DATE` 나 `DATETIME` 과 같은 시간관련 함수에서는 문자열 형태로 써준다.
<br>

## 데이터 정렬
- `ORDER` : 순서
- `BY` : ~에 의해
- `ASC` : 오름차순 정렬 (ascending)
- ASC를 입력하지 않아도 **기본적으로 오름차순 정렬**을 한다.

작성한 컬럼 순서대로 정렬이 된다.

```sql
SELECT * FROM member
ORDER BY height ASC;
```

```sql
SELECT email, sign_up_day FROM member
ORDER BY YEAR(sign_up_day) DESC, email ASC;
```

숫자값이 담긴 컬럼을 정렬 기준으로 할 때는 그 컬럼의 **데이터 타입이 숫자형인지, 문자열형인지**에 주의해야 한다.  1이라고 입력되어 있지만 `INT` 1이 아닌 `TEXT` ”1”일 수도 있기 때문이다.

- `CAST` : 데이터 타입을 바꿀 때 사용된다.
- `decimal` : 소수점

```sql
SELECT * FROM member
ORDER BY CAST(data AS signed) ASC;
```
<br>

## 데이터 일부만 추출

- `LIMIT` : 제한, 한도
- `LIMIT 10` : 0~9번째 row만 추출

```sql
SELECT * FROM member
ORDER BY sign_up_day DESC
LIMIT 10;
```

```sql
SELECT * FROM member
ORDER BY sign_up_day DESC
LIMIT 8, 2
```

---

## 집계함수

### COUNT()

```sql
SELECT COUNT(*) FROM member;
```

### MAX()

```sql
SELECT MAX(height) FROM member;
```

### MIN()

```sql
SELECT MIN(height) FROM member;
```

### AVG()

`AVG()` 함수는 **NULL이 있는 row는 제외**하고 평균을 계산한다.

```sql
SELECT AVG(height) FROM member;
```

### SUM()

```sql
SELECT SUM(height) FROM member;
```

### STD()

```sql
SELECT STD(height) FROM member;
```

## 산술함수

### ABS()

```sql
SELECT ABS(age) FROM member;
```

### SQRT()

```sql
SELECT SQRT(age) FROM member;
```

### CEIL()

```sql
SELECT CEIL(age) FROM member;
```

### FLOOR()

```sql
SELECT FLOOR(age) FROM member;
```

### ROUND()

```sql
SELECT ROUND(age) FROM member;
```
<br>

## 📝 집계 함수와 산술 함수의 차이점
- `집계 함수`는 특정 컬럼의 **여러 row 값들을 동시에 고려해서 실행**되는 함수
- `산술 함수`는 특정 컬럼의 **각 row 값마다 실행**되는 함수
<br>

## 📝 NULL에 관한 주의사항
- IS NULL 과 = NULL은 다르다.
- `NULL`은 어떤 값이 아니기 때문에 등호(=)를 사용해서 어떤 값과 **비교할 수 있는 대상이 아니다**.
- **NULL인지를 확인**할 때는 반드시 `IS NULL` 을 사용해야 한다.
- NULL에는 어떤 연산을 해도 결국 NULL이다.
- NULL에는 +, -, *, / 등 무엇을 하든 **항상 NULL**이다.
<br>

## alias
- `alias`는 원래의 컬럼 이름을 다른 이름으로 교체해서 보여주는 기능을 한다.
- `AS 바꿔줄 이름` 혹은 `(띄어쓰기 1칸) 바꿔줄 이름`으로 사용한다.

```sql
SELECT
    email,
    height AS 키,
    weight AS 몸무게,
    weight / ((height/100) * (height/100)) AS BIM
FROM member;
```
<br>

## 고유값

- `DISTINCT()` : 중복 값들을 제외하고 고유한 값만 보는 방법이다.
- `SUBSTRING()` : 문자열의 일부 추출한다.

```sql
SELECT DISTINCT(gender) FROM member;
```

```sql
SELECT DISTINCT(SUBSTRING(address, 1, 2)) FROM member;
```

---

## GROUPING
- `그루핑`이란 row들을 여러 개 그룹으로 나누는 것을 말한다.
- 그루핑은 **여러 개의 컬럼** 사용이 가능하다.
- `HAVING` : 여러 그룹들 중 보고 싶은 그룹만 조회하는 함수
- HAVING에는 여러 조건이 입력 가능하다.
- `HAVING` 대신 `WHERE`를 입력하면 오류가 난다. 둘은 비슷해 보이지만 엄연히 다르다.
- `WHERE`는 테이블에서 맨 처음 row들을 조회할 때 조건 설정한다.
- `HAVING`은 이미 조회된 row들을 그루핑했을 때, 그 그룹들 중에서 다시 필터링한다.

예를들어 남성 회원과 여성 회원들이 각각 총 몇 명인지를 알기 위해서 먼저 **성별 기준으로 그루핑**을 해야 한다.

```sql
SELECT gender, COUNT(*) FROM member GROUP BY gender;
```

```sql
SELECT
    SUBSTRING(address, 1, 2) AS region,
    gender,
    COUNT(*)
FROM member
GROUP BY
    SUBSTRING(address, 1, 2),
    gender;
```

```sql
SELECT
    SUBSTRING(address, 1, 2) AS region,
    gender,
    COUNT(*)
FROM member
GROUP BY
    SUBSTRING(address, 1, 2),
    gender
HAVING region = '서울';
```
<br>

# GROUP BY 규칙
`GROUP BY`를 사용할 때 `SELECT` 절에는 아래 두 가지만 사용할 수 있다는 규칙이 있다.

- `GROUP BY` 뒤에서 사용한 컬럼들
- `COUNT`, `MAX` 등 `집계 함수`
