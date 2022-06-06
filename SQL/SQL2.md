# Today I Learned - 2022/05/20 Fri

# 조건문

## CASE

CASE 함수에는  크게 두 종류가 있다. `단순 CASE`와 `검색 CASE` 함수로 나뉜다.

- `CASE` : 사건, 경우
- `WHEN` : 조건
- `THEN` : 반환할 값
- `ELSE` : 지금까지 경우를 제외한 나머지 경우
- `END` : CASE문 종료
- `CASE`와 `END`에 괄호()를 씌워 `AS 컬럼명` 지정 가능
<br>

### 1. 단순 CASE

CASE문 바로 뒤에 컬럼 이름을 쓰고, 그 컬럼의 값과 어떤 값이 **같은지(=)**를 비교하는 CASE 함수를 의미한다.

💻 문법

```sql
CASE 컬럼 이름
  WHEN 값 THEN 값
  WHEN 값 THEN 값
  WHEN 값 THEN 값
  ELSE 값
END

```

💻 예시

```sql
SELECT email,
(CASE age
	WHEN 29 THEN '스물 아홉 살'
	WHEN 30 THEN '서른 살'
	ELSE age
END)
FROM member;
```
<br>

### 2. 검색 CASE
사용자가 직접 **조건을 설정**하여 THEN 뒤의 값을 반환한다.

💻 문법

```sql
CASE
  WHEN 조건1 THEN 값
  WHEN 조건2 THEN 값
  WHEN 조건3 THEN 값
  ELSE 값
END
```

💻 예시
```sql
SELECT
	email,
	CONCAT(height, 'cm', ', ', weight, 'kg') AS '키와 몸무게',
	weight / ((height/100) * (height/100)) AS BIM,
	(CASE
		WHEN weight IS NULL OR height IS NULL THEN '비만 여부 알 수 없음'
		WHEN weight / ((height/100) * (height/100)) >= 25 THEN '과제충 또는 비만'
    		WHEN weight / ((height/100) * (height/100)) >= 18.5
			AND  weight / ((height/100) * (height/100)) < 25 THEN '정상'
		ELSE '저체중'
	END) AS obesity_check
FROM member
ORDER BY obesity_check ASC;
```
<br>

## IF

- height가 NULL이 아닌 경우 height 값 그대로 반환, NULL이면 'N/A' 반환

```sql
SELECT IF(height IS NOT NULL, height, 'N/A') FROM copang_main.member;
```

## COALESCE

- NULL 값을 'N/A'로 반환

```sql
SELECT COALESCE(height, 'N/A') FROM copang_main.member;
```

- NULL 값을 weight * 2.3으로 계산하고, 둘 다 NULL일 경우 'N/A' 반환

```sql
SELECT COALESCE(height, weight * 2.3, 'N/A') FROM copang_main.member;
```

## IFNULL

- height가 NULL이면 'N/A'를 출력하고, NULL이 아니면 컬럼 값 그대로 반환

```sql
SELECT IFNULL(height, 'N/A') FROM copang_main.member;
```
<br>

# 문자열 관련 함수

## LENGTH

- `LENGTH` : 문자열 길이를 나타낸다.

```sql
SELECT LENGTH(address) FROM member;
```

## UPPER / LOWER

- `UPPER`는 문자열을 모두 대문자로 바꿔준다.
- `LOWER`는 문자열을 모두 소문자로 바꿔준다.

```sql
SELECT email, UPPER(email) FROM member;
SELECT email, LOWER(email) FROM member;
```

## LPAD / RPAD

- `LPAD`는 왼쪽을 특정 문자열로 채워준다.
- `RPAD`는 오른쪽을 특정 문자열로 채워준다.
- 10은 10개를 새로운 문자열로 채우는 게 아닌 문자열의 총 길이가 10개임을 의미한다.

```sql
SELECT age, LPAD(age, 10, '0') FROM member;
SELECT age, RPAD(age, 10, '0') FROM member;
```
<br>

ex)
- 28 ⇒ 0000000028
- 28 ⇒ 2800000000
<br>

<aside>
❗ 위처럼 INT형 컬럼에 문자열 함수를 통해 “0”을 추가시키면 자동으로 컬럼의 type이 문자열로 형 변환이 된다.

</aside>

<br>

## TRIM / LTRIM / RTRIM

- `LTRIM`은 왼쪽 공백을 삭제한다.
- `RTRIM`은 오른쪽 공백을 삭제한다.
- `TRIM`은 왼쪽, 오른쪽(양쪽) 공백을 삭제한다.

```sql
SELECT LTRIM(word) FROM test;
SELECT RTRIM(word) FROM test;
SELECT TRIM(word) FROM test;
```
