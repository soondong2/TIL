# Today I Learned - 2022/05/13 Fri

# 표본추출(Sampling)

## 표본조사(Sample Survey)
- 집단의 구성원 모두를 조사하는 `전수조사`와 일부를 표본으로 하는 `표본조사`가 있다.

## 장점
- 시간과 비용을 절약할 수 있다.
- 잘 훈련된 요원에 의한 조사는 비표본 오차를 줄여 경우에 따라서는 전수조사보다 정확한 자료를 획득할 수 있다.

## 단점
- 표본설계가 복잡한 경우 시간과 비용이 낭비될 수 있다.
- 표본의 대표성 문제가 제기되면 일반화의 가능성은 낮아진다.
- 크기가 작을 경우에는 표집 자체가 무의미하다.

## 용어
- `모집단(Population)` : 조사하고자 하는 대상집단의 전체
- `원소(Element)` : 모집단을 구성하는 개체
- `모수(Parameter)` : 표본 관측에 의해 구하고자 하는 정보
- `표집틀(Sample Frame)` : 표본추출단위가 수록된 목록

## 표본추출 과정
모집단 결정, 표집틀 선정, 표본추출방법 결정, 표본 크기 결정, 표본추출의 순서

## 표본추출 방법
`확률 표본추출`과 `비확률 표본추출`로 구분된다.

### 확률 표본추출법
모집단으로부터 동일한 확률로 표본의 원소들을 추출하는 방법이다.  
`무작위(Random)` 추출로 각 원소가 뽑힐 확률은 동일하므로 모집단을 대표할 수 있는 표본을 추출할 가능성이 높다.

1) 단순랜덤추출법
  - N개의 모집단에서 n개의 표본을 추출하고자할 때, 추출될 가능성을 동일하게 해주는 표본추출 방법이다.
2) 계통추출법
  - `K개`씩 `n개`의 구간으로 나누고 첫 구간에서 하나를 랜덤하게 출발점으로 정한 다음, `매 k번째` 떨어진 간격에 위치하는 원소들을 표본으로 추출한다.
  - k는 `N/n`의 이하가 되도록 정해준다.
3) 집락추출법
  - 몇 개의 집단이 결합된 형태로 구성되어 있고 일련번호를 부여할 수 있는 경우에 이용되는 표본추출 방법이다.
  - 집단을 집락이라고하며 **집단 내는 이질적**, **집단 간은 동질적**이다.
4) 층화추출법
  - 이질적인 원소들로 구성된 모집단에서 각 계층을 대표할 수 있도록 표본을 추출하는 방법이다.
  - 모집단을 **서로 겹치지 않는 층들로 나누고 각 층에서 단순확률표본을 추출**하는 방법이다.
  - **집단 내는 동질적**, **집단 간은 이질적**이다.

### 비확률 표본추출법
작위적 표본추출로 일반화에는 제약이 있다.

1) 편의 표본추출
  - 정해진 크기의 표본을 선정할 때까지 임의로 원소들을 표집한다.
2) 유의(판단) 표본추출
  - 전문가나 특정 조직 등 제한된 특정 대상들만으로 표본을 추출한다.
3) 할당 표본추출
  - 모집단 속성을 미리 파악할 수 있을 때 각 속성의 `비율`을 고려해 표본을 추출한다.
4) 눈덩이 표본추출
  - `소수` 참여 대상자로부터 `소개`받는 식으로 누적해가는 방법이다.

## 측정
|척도|정의|예시|
|:---:|:---:|:---:|
|명목척도|측정 대상이 **어느 집단에 속하는지 분류**|성별, 출생지, 선수 등 번호|
|순서척도|측정 대상의 **서열관계**를 측정하는 척도|만족도, 선호도, 학년, 신용등급|
|구간척도|측정 대상이 갖고 있는 **속성의 양**을 측정하는 것으로 **간격이 의미가 있는 자료**|온도, 지수|
|비율척도|간격에 대한 비율이 의미를 가지는 자료, **절대적 기준인 0이 존재**하고 **사칙연산**이 가능|무게, 나이, 거리, 시간|

