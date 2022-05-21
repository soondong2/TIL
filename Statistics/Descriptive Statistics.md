# Today I Learned - 2022/05/15 Sun

# 기술통계(Descriptive Statistics)
자료의 특성을 표, 그림, 통계량 등을 사용하여 쉽게 파악할 수 있도록 정리하고 요약하는 걸 의미한다.

## 중심위치의 측도
### 표본평균(sample mean)
- 극단값에 영향을 받는다.

### 중앙값(median)
- 평균에 비해 극단값에 영향을 덜 받는다.
- 홀수 : (n+1) / 2
- 짝수 : (n / 2)번째 값과 (n / 2) + 1번째 값의 평균
  
## 산포의 측도
### 분산(variance)
- 변수의 흩어진 정도를 계산하는 지표

### 표준편차(standard deviation)
- 자료가 평균을 중심으로 얼마나 퍼져 있는지를 나타내는 대표적인 수치이다.
- 표준편차가 0에 가까우면 자료 값들이 평균 근처에 몰려있다는 의미이다.

### 사분위수범위
```
IQR = Q3 - Q1
```

### 사분위수
- 제 1사분위수(`Q1`) = `25`백분위수
- 제 2사분위수(`Q2`) = `50`백분위수 = `중위수`
- 제 3사분위수(`Q3`) = `75`백분위수

### 변동계수(coefficient of variation)
```
CV = 표준편차 / 표본평균
```
### 평균의 표준오차
```
SE(X) = 표분편차 / sqrt(n)
```

## 분포의 형태에 관한 측도
### 왜도
- 분포의 `비대칭정도`를 나타내는 측도이다.
- `왜도 < 0` : 왼쪽으로 긴 꼬리를 갖는 분포이다.
- `왜도 = 0` : 좌우가 대칭인 분포이다.
- `왜도 > 0` : 오른쪽으로 긴 꼬리를 갖는 분포이다.

### 첨도
- 분포의 중심에서 `뾰족한 정도`를 나타내는 측도이다.
- `첨도 < 0` : 표준정규분포보다 더 뾰족하다.
- `첨도 = 0` : 표준정규분포와 유사하다.
- `첨도 > 0` : 표준정규분포보다 덜 뾰족하다.

## 그래프
### 히스토그램
- 표로 되어 있는 도수 분포를 그림으로 나타낸 것으로, 도수분포표를 그래프로 나타낸 것이다.
- 계급의 간격은 (최대값 - 최소값) / 계급수로 파악할 수 있다.
- 계급의 수와 간격이 변하면 히스토그램의 모양이 변한다.

||막대그래프|히스토그램|
|:---:|:---:|:---:|
|차이점|**범주형**으로 구분된 데이터를 표현하며 범주의 순서를 의도에 따라 바꿀 수 있다.|**연속형** 데이터를 표현하며 순서를 바꿀 수 없고 막대의 간격이 없다.|

### 상자그림(Box plot)
- 최소값, 최대값, Q1, Q2, Q3
- 사분위수범위(IQR) : Q3 - Q1
- 안울타리 : Q1 - 1.5 x IQR 또는 Q3 + 1.5 x IQR
- 바깥울타리 : Q1 - 3 x IQR 또는 Q3 + 3 x IQR
- 보통이상점 : 안쪽 울타리와 바깥 울타리 사이에 있는 자료
- 극단이상점 : 바깥 울타리 밖의 자료
