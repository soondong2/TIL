# Today I Learned - 2022/09/27 Tue

# 다중선형회귀분석(Multiple Linear Regression Analysis)
- 독립변수가 두 개 이상인 경우에 쓰는 선형회귀분석이다
- y = b0 + b1x1 + b2x2 + ... + bkxk + e
<br>

## 모형의 통계적 유의성
- 모형의 통계적 유의성은 **F통계량**으로 확인한다.
- 귀무가설 : b1 = b2 = ... = bk
- 대립가설 : 적어도 하나는 다르다.
- F통계량의 p-value가 유의수준보다 작으면 귀무가설을 기각한다.
<br>

|요인|제곱합|자유도|제곱평균|F-통계량|
|:---:|:---:|:---:|:---:|:---:|
|회귀|SSR|k|MSR|F|
|오차|SSE|n-k-1|MSE||
|계|SST|n-1|||
<br>

## 회귀계수의 유의성
- 단변량 회귀분석과 같이 t통계량을 확인한다.
<br>

## 모형의 설명력
- 결정계수 또는 수정된 결정계수를 확인한다.
<br>

## 모형의 적합성
- 잔차와 종속변수의 산점도로 확인한다.
<br>

## 데이터가 전제하는 가정을 만족시키는가?
- 선형성, 독립성, 등분산성, 비상관성, 정규성
<br>

## 다중공선성(Multicollinearity)
- 다중회귀분석에서 설명변수들 사이에 선형관계가 존재하면 회귀계수의 정확한 추정이 곤란하다.
- `분산팽창요인(VIF)` : 4보다 크면 다중공선성이 존재한다고 볼 수 있고, 10보다 크면 심각한 문제가 있다고 해석할 수 있다.
- `상태지수` : 10 이상이면 문제가 있다고 보고, 30 보다 크면 심각한 문제가 있다고 해석할 수 있다.
- 문제가 있는 변수를 제거하거나 주성분회귀, 능형회귀 모형을 적용하여 문제를 해결할 수 있다.