# Today I Learned - 2022/05/27 Fri

# JOIN
`JOIN`은 서로 다른 테이블을 합쳐 하나로 만드는 것이다.
<br>

# 결합연산
- `결합 연산` : 테이블을 **가로 방향**으로 합치는 것에 관한 연산

## LEFT OUTER JOIN
- `LEFT OUTER JOIN`은 LEFT OUTER JOIN의 왼쪽에 있는 테이블을 기준으로 오른쪽에 있는 테이블을 합친다.
- `ON` 뒤의 기준으로 합친다.

```sql
SELECT
    item.id,
    item.name,
    stock.item_id,
    stock.inventory_count
FROM item LEFT OUTER JOIN tock
ON item.id = stock.item_id;
```
<br>

## RIGHT OUTER JOIN
- `RIGHT OUTER JOIN`은 RIGHT OUTER JOIN의 오른쪽에 있는 테이블을 기준으로 왼쪽에 있는 테이블을 합친다.
- `ON` 뒤의 기준으로 합친다.

```sql
SELECT
    item.id,
    item.name,
    stock.item_id,
    stock.inventory_count
FROM item RIGHT OUTER JOIN stock
ON item.id = stock.item_id;
```
<br>

## INNER JOIN
`INNER JOIN`은 각 테이블에서 조인 기준으로 사용된 컬럼들의 일치하는 값이 둘 다 존재하는 row들만 합친다. 기준이 되는 테이블은 따로 존재하지 않는다.

```sql
SELECT
    i.id,
    i.name,
    s.item_id,
    s.inventory_count
FROM item AS i INNER JOIN stock AS s
ON i.id = s.item_id;
```
<br>

## alias

- 테이블에도 `alias`를 붙일 수 있다..
- 테이블에 `alias`를 붙일 경우 SQl문에서 테이블 이름이 등장하는 다른 부분들도 다 `alias`로 바꿔줘야 한다.
- JOIN을 하는 SQL문은 길이가 꽤 길기 때문에 `JOIN`과 함께 `alias`를 자주 사용한다.

```sql
SELECT
    i.id,
    i.name,
    s.item_id,
    s.inventory_count
FROM copang_main.item AS i RIGHT OUTER JOIN copang_main.stock AS s
ON i.id = s.item_id;
```
<br>

## ON / USING

- JOIN 조건으로 쓰인 두 컬럼의 이름이 같다면 ON 대신 `USING`을 쓴다.

```sql
SELECT
    old.id AS old_id,
    old.name AS old_name,
    new.id AS new_id,
    new.name AS new_name
FROM item AS old INNER JOINitem_new AS new
ON old.id = new.id;
```

```sql
SELECT
    old.id AS old_id,
    old.name AS old_name,
    new.id AS new_id,
    new.name AS new_name
FROM item AS old INNER JOIN item_new AS new
USING(id);
```
<br>

# 집합연산

- `집합 연산` : 테이블을 **세로 방향**으로 합치는 것에 관한 연산
- 서로 다른 종류의 테이블도 조회하는 컬럼을 일치시키면 집합 연산이 가능하다.
- 컬럼 구조가 같은 테이블끼리만 UNION 연산을 할 수 있다.
- SELECT 절 뒷 부분을 두 테이블이 공통적으로 갖고 있는 컬럼 이름들로 바꿔주면 된다.

- 집합 연산 중 `INTERSECT`, `MINUS` 연산자는 MySQL에서 지원하지 않기 때문에 `JOIN`을 통해 간접적으로 원하는 결과를 얻어야 한다.
<br>

## UNION

- `UNION`은 **중복을 제거**하고 하나의 row만 보여준다.

```sql
SELECT
    id,
    nation,
    count
FROM Summer_Olympic_Medal
UNION
FROM Winter_Olympic_Medal;
```
<br>

## UNION ALL

- `UNION ALL`은 **중복을 제거하지 않고** 합친다.

```sql
SELECT
    id,
    nation,
    count
FROM Summer_Olympic_Medal
UNION ALL
FROM Winter_Olympic_Medal;
```
<br>

## NATURAL JOIN

- 두 테이블에서 같은 이름의 컬럼을 찾아서 자동으로 조인 조건을 설정하고 INNER JOIN 해주는 조인이다. `자연 조인`이라고도 한다.
- 자동으로 조인 조건을 찾아서 조인하기 때문에 조인 기준을 설정하는 `ON`절을 입력하지 않아도 된다.

```sql
SELECT
    p.id,
    p.player_name,
    p.team_name,
    t.team_name,
    t.region
FROM player AS p NATURAL JOIN team AS t;
```
<br>

## CROSS JOIN

한 테이블의 하나의 row에 다른 테이블의 모든 row들을 매칭하고, 그 다음 row에서도 또 다른 테이블의 모든 row들을 매칭하는 것을 반복함으로써 두 테이블의 row들을 모든 조합으로 보여주는 조인이다.

```sql
SELECT * FROM member CROSS JOIN stock
```
<br>

## SELF JOIN

- 자기 자신과 조인하는 경우를 말한다.

```sql
SELECT * FROM member AS m1 LEFT OUTER JOIN member AS m2
ON m1.age = m2.age;
```
<br>

## FULL OUTER JOIN

- 두 테이블의 LEFT OUTER JOIN 결과와 RIGHT OUTER JOIN 결과를 합치는 조인이다. 대신 두 결과에 존재하는 공통 row들은 한 번만 표현해준다.

- LEFT OUTER JOIN과 RIGHT OUTER JOIN을 `UNION`으로 중복 제거해준다.
- Oracle이라는 DBMS에는 FULL OUTER JOIN 연산자가 내장되어 있다.
<br>

## Non-Equi JOIN

- 조인 조건에 **등호(=)**를 사용하는 조인을 `Equi` 조인이라고 한다.
- `Non-Equi` 조인은 동등 조건이 아닌 다른 종류의 조건을 사용해서 조인한다.

```sql
SELECT
    m.email,
    m.sign_up_day,
    i.name,
    i.registration_date
FROM member AS m LEFT OUTER JOIN item AS i
ON m.sign_up_day < i.registration_Date
ORDER BY m.sign_up_day ASC;
```
