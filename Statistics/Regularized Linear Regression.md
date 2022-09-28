# Today I Learned - 2022/09/28 Wed

# 정규화 선형회귀(Regularized Linear Regression)
- 정규화 선형회귀는 **선형회귀 계수에 대한 졔약 조건을 추가하여 모델이 과도하게 최적화되는 현상(과적합, Overfitting)을 막는 방법**이다.
- **Ridge 회귀, Lasso 회귀, Elastic Net** 회귀모형이 일반적으로 사용된다.
<br>

## 1. 라쏘회귀(Lasso Regression)
- **가중치 절대값의 합을 최소화하는 것을 제약조건으로 추가**하는 기법이다.
- 가중치가 0에 가까워질 뿐, 실제로 0이 되지는 않는다.
- **L1규제(Penalty)** 라고 한다.
<br>

## 2. 릿지회귀(Ridge Regression)
- **가중치들의 제곱합을 최소화하는 것을 제약조건으로 추가하는 기법**이다.
- 중요하지 않은 가중치는 0이 될 수도 있다.
- **L2규제(Penalty)** 라고 한다.
<br>

## 3. 엘라스틱넷(Elastic Net)
- 릿지회귀와 라쏘회귀를 결합한 모델이다.
- lambda1과 lambda2라는 두 개의 하이퍼 모수를 가진다.
