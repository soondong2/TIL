# Today I Learned - 2022/12/19 Mon

## 윈도우 함수(Window Function)
- 그룹 함수들에 대해서 데이터 처리를 간단하게 하기 위한 함수이다.
- 윈도우 함수는 중첩해서 사용할 수 없다.
- 윈도우 함수는 `OVER` 구문이 **필수로 포함**되어야 한다.
- 윈도우 함수를 `OLAP` 함수라고도 한다.

### 윈도우 함수 분류
|분류|종류|
|:---:|:---:|
|순위 함수|그룹 내의 순위를 계산하는 함수, `RANK`, `DENSE__RANK`, `ROW_NUMBER`|
|집계 함수|그룹 내의 값을 집계하는 함수, `SUM`, `MAX`, `MIN`, `AVG`, `COUNT`|
|순서 함수|그룹 내의 행의 순서를 구하는 함수, `FIRST_VALUE`, `LAST_VALUES`, `LAG`, `LEAD`|
|비율 함수|그룹 내의 비율을 구하는 함수, `CUME_DIST`, `PERCENT_RANK`, `NTILE`, `RATIO_TO_REPORT`|

### 윈도우 함수 문법
```sql
SELECT
  WINDOW_FUNCTION(ARGUMENTS)
  OVER(
    [PARTITION BY 컬럼]
    [ORDER BY 절]
    [WINDOWING 절]
  )
 FROM 테이블명;
```
- `WINDOW_FUNCTION` : 함수명
- `ARGUMENTS(인수)` : 함수에 따라 0 ~ N개의 인수가 지정될 수 있다.
- `PARTITION BY 절` : 전체 집합을 기준에 의해 소그룹으로 나눌 수 있다.
- `ORDER BY 절` : 어떤 항목에 대해 순위를 지정할 지 ORDER BY절을 기술한다.

<br>

### 그룹 내 순위(RANK) 관련 함수
#### RANK
- ORDER BY를 포함한 쿼리문에서 **특정 컬럼에 대한 순위**를 구하는 함수이다.
- 동등한 순위가 나왔을 때 동등한 순위 수만큼 **건너 뛰고** 순위를 계산한다. ex) 1, 2, 3, 3, 5

#### DENSE_RANK
- RANK 함수와 비슷하지만, **동일한 순위를 하나의 건수로 취급한다.**
- 동등한 순위가 나왔을 때 바로 다음 순위가 나온다. ex) 1, 2, 3, 3, 4

#### ROW_NUMBER
- RANK나 DENSE_RANK 함수가 동일한 값에 대해 동일한 순위를 부여하는데에 반해, **동일한 값이더라도 고유한 순위를 부여**한다.
- 동등한 순위를 무시한다. ex) 1, 2, 3, 4

<br>

|학번|학과|이름|점수|
|:---:|:---:|:---:|:---:|
|1000|전산|철수|70|
|2000|전기|영준|85|
|3000|전자|진호|95|
|4000|전산|영진|100|
|5000|전자|현영|85|
<br>

```sql
SELECT
  학번, 이름, 점수, 
  RANK() OVER(ORDER BY 점수 DESC) AS '순위1',
  DENSE_RANK() OVER(ORDER BY 점수 DESC) AS '순위1',
  ROW_NUMBER() OVER(ORDER BY 점수 DESC) AS '순위3'
FROM 학생;
```
|학번|이름|점수|순위1|순위2|순위3|
|:---:|:---:|:---:|:---:|:---:|:---:|
|4000|영진|100|1|1|1|
|3000|진호|95|2|2|2|
|5000|현영|85|3|3|3|
|2000|영준|85|3|3|4|
|1000|철수|70|5|4|5|

<br>

### 그룹 내 행 순서 관련 함수
#### FIRST_VALUE
- 파티션별 윈도우에서 **가장 먼저 나온 값**을 구한다.
- MIN 함수를 활용하여 같은 결과를 얻을 수 있다.

#### LAST_VALUE
- 파티션별 윈도우에서 **가장 나중에 나온 값**을 구한다.
- MAX 함수를 활용하여 같은 결과를 얻을 수 있다.

#### LEAD
- 파티션별 윈도우에서 이후 몇 번째 행의 값을 가져올 수 있다.
- 즉, `아래`에 있는 값을 가져온다.

#### LAG
- 파티션별 윈도우에서 이전 몇 번째 행의 값을 가져올 수 있다.
- 두 번째 인자는 몇 번째 앞의 행을 가져올 지 결정한다.
- 세 번째 인자는 값이 없을 때 다른 값으로 변경한다.
- 즉, `위`에 있는 값을 가져온다.

<br>

- `FIRST_VALUE`, `LAST_VALUE` 사용 예시
```sql
SELECT
  학번, 이름, 점수,
  FIRST_VALUE(이름) OVER(ORDER BY 점수 DESC) AS F_VAL,
  LAST_VALUE(이름) OVER(ORDER BY 점수 DESC) AS L_VAL
FROM 학생;
```
|학번|이름|점수|F_VAL|L_VAL|
|:---:|:---:|:---:|:---:|:---:|
|4000|영진|100|영진|철수|
|3000|진호|95|영진|철수|
|5000|현영|85|영진|철수|
|2000|영준|85|영진|철수|
|1000|철수|70|영진|철수|

<br>

- `LEAD`, `LAG` 사용 예시
```sql
SELECT
  학번, 이름, 점수,
  LAG(이름) OVER(ORDER BY 점수 DESC) AS LAG,
  LEAD(이름) OVER(ORDER BY 점수 DESC) AS LEAD
FROM 학생;
```
|학번|이름|점수|LAG|LEAD|
|:---:|:---:|:---:|:---:|:---:|
|4000|영진|100|NULL|진호|
|3000|진호|95|영진|현영|
|5000|현영|85|진호|영준|
|2000|영준|85|현영|철수|
|1000|철수|70|영준|NULL|

<br>

### 그룹 내 비율 관련 함수
#### CUME_DIST
- 파티션별 윈도우의 전체 건수에서 현재 행보다 작거나 같은 건수에 대한 `누적백분율`을 구한다.

#### PERCENT_RANK
- 파티션별 윈도우에서 제일 먼저 나오는 것을 0으로, 제일 늦게 나오는 것을 1로 하여, 값이 아닌 행의 순서별 `백분율`을 구한다.

#### NTILE
- 파티션별 전체 건수를 인수 값으로 `N등분`한 결과를 구할 수 있다.
- NTILE을 활용하면 등분하여 순위를 매길 수 있다.
- NTILE(3) : 상중하
- NNTILE(2) : 상위, 하위

#### RATIO_TO_REPORT
- 파이션 내 전체 SUM(컬럼) 값에 대한 행별 컬럼 값의 백율을 소수점으로 구할 수 있디.
