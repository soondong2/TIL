# Today I Learned - 2022/05/11 Fri

#  데이터베이스란 ❓
데이터베이스란 입문자 관점에서 보면 구체적인 이미지를 잡기가 어려워서 학습과 관련된 사항을 찾기가 어려운 분야이다. 프로그래밍 언어나 웹 사이트 구현 등은 목적이 분명하고 쉽게 접근하여 배울 수 있는 것과는 대조적이다. `데이터를 모으는 장소` 라고 상상하긴 하지만, 그 이상의 무엇을 하는지를 표현하기가 매우 모호하다는 것이 데이터베이스의 어려움이다. 또한 데이터베이스는 주소록에서 시작되었다.
<br>

## “DB 어떤거 써보셨어요?”
- `MySQL` 써봤습니다. 
- `데이터베이스` 라는 말을 들으면 **`데이터를 관리하는 프로그램` + `그 안에 저장된 데이터`** 를 합해서 말하는 거라고 생각하면 된다. 
<br>

# 데이터베이스의 기본 기능
## 1. 데이터베이스의 갱신

데이터베이스의 가장 중요한 기능은 `검색` 이다. 검색은 `추출` , `질의` 라고도 한다.
<br>

## 2. 데이터베이스의 동시성 제어
개인이 관리하는 주소록은 검색, 갱신을 하는 사람이 1명이다. 그러나 비즈니스 목적으로 이용되는 데이터베이스에는 많은 사용자가 동시에 접근한다. 즉, 데이터베이스는 동시에 여러 사용자로부터 검색, 갱신 처리를 받는다. 이때 다양한 상황들이 발생하게 됩니다.

1. 최초로 파일을 연 사람이 파일을 열고 있을 때 그 다음 사람은 파일을 열 수 없다. 
2. 최초로 파일을 연 사람이 파일을 열고 있을 때 그 다음 사람은 읽기 전용으로만 열 수 있다.
3. 모든 사람이 파일을 열 수 있고 나중에 수행된 쪽의 갱신이 반영된다.
<br>

## 3. 데이터베이스의 장애 대응
외부의 공격으로 고객들의 개인정보가 전부 사라졌다고 생각해보자. 이걸 **데이터가 날아갔다** 라고도 표현한다.
데이터베이스는 데이터를 한 곳이 아니라 복수의 장소에 `분산` 해서 저장하는 등 데이터를 보호하고, 장애에 대응할 수 있어야 한다.
<br>

## 4. 데이터베이스의 보안
은행 데이터베이스를 통해 내 계좌에 돈이 얼마나 들어있는지는 볼 수 있지만, 그 데이터베이스가 남들 계좌에 돈이 얼마나 들어있는지까지 보여주지는 않는다. 해킹 등 외부의 자극에도 뚫리지 않아야 한다.

<br>

# 데이터베이스의 갱신
데이터베이스의 가장 중요한 기능은 `검색` 이다. 검색은 `추출` , `질의` 라고도 한다.

<br>

## 1. 데이터베이스의 동시성 제어
개인이 관리하는 주소록은 검색, 갱신을 하는 사람이 1명이다. 그러나 비즈니스 목적으로 이용되는 데이터베이스에는 많은 사용자가 동시에 접근한다. 즉, 데이터베이스는 동시에 여러 사용자로부터 검색, 갱신 처리를 받는다. 이때 다양한 상황들이 발생하게 됩니다.


1. 최초로 파일을 연 사람이 파일을 열고 있을 때 그 다음 사람은 파일을 열 수 없다. 
2. 최초로 파일을 연 사람이 파일을 열고 있을 때 그 다음 사람은 읽기 전용으로만 열 수 있다.
3. 모든 사람이 파일을 열 수 있고 나중에 수행된 쪽의 갱신이 반영된다.
<br>

## 2. 데이터베이스의 장애 대응
외부의 공격으로 고객들의 개인정보가 전부 사라졌다고 생각해보자. 이걸 **데이터가 날아갔다** 라고도 표현한다.

데이터베이스는 데이터를 한 곳이 아니라 복수의 장소에 `분산` 해서 저장하는 등 데이터를 보호하고, 장애에 대응할 수 있어야 한다.
<br>

## 3. 데이터베이스의 보안
은행 데이터베이스를 통해 내 계좌에 돈이 얼마나 들어있는지는 볼 수 있지만, 그 데이터베이스가 남들 계좌에 돈이 얼마나 들어있는지까지 보여주지는 않는다. 해킹 등 외부의 자극에도 뚫리지 않아야 한다.

<br>

# 데이터베이스의 종류
`RDB` (Relational Database), `RDBMS` (Relation Database Management System)이라고도 부른다.

<br>

### 1. 관계형 데이터베이스 ⭐⭐⭐
**`2차원 표 형식` 으로 관리하는 데이터베이스**. 현재 가장 주류를 이루고 있으며 우리 수업에서 다루는 MySQL도 이 관계형 데이터베이스이다. 아무런 수식어 없이 `데이터베이스` 라고 부른다면 보통 이 구조를 말한다.

### 2. NoSQL 데이터베이스 ⭐
NoSQL은 `Not Only SQL` 의 줄임말으로 여기에서 `SQL` 이란 관계형 데이터베이스 언어를 의미한다. 대량의 데이터를 고속으로 처리해야하는 웹 서비스에서 최근 자주 사용되고 있다.

### 3. 계층형 데이터베이스
데이터를 계층 구조로 관리하는 데이터베이스. 예를 들면, 조직도가 있다.
