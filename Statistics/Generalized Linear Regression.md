# Today I Learned - 2022/09/28 Wed

# 일반화 선형회귀(GLM, Generalized Linear Regression)
- 회귀분석은 연속형의 종속변수가 정규분포를 따른다는 정규성을 가정한다. 하지만 종속변수가 범주형 자료이거나 정규성을 만족하지 못하는 경우도 있다.
- 이러한 경우에 **종속변수를 적절한 함수로 변화시켜 f(x)를 정의한 후, 이 f(x)와 독립변수를 선형결합으로 모형화하는 일반화 선형모형(glm)** 을 이용한다.
- 일반화 선형모형은 3가지 성분에 의해서 정의된다.
<br>

|성분|설명|
|:---:|:---:|
|랜덤성분|종속변수의 확률분포를 규정하는 성분|
|체계적 성분|E(y)를 정의하는 설명변수들 간의 선형결합(선형식)|
|연결함수|랜덤성분과 체계적 성분을 연결하는 함수|
<br>

- 랜덤성분 체계적 성분, 연결함수에 따른 glm 분석 방법은 다음과 같다.
<br>

|랜덤성분(반응변수)|연결함수|치계적 성분(설명변수)|분석방법(Model)|
|:---:|:---:|:---:|:---:|
|Normal|Identity|연속형|Regression|
|Normal|Identity|범주형|ANOVA|
|Normal|Identity|연속형+범주형|Regression with Indicator ANCOVA|
|Binomial|Logit|연속형+범주형|Logistic Regression|
|Poisson|Log|연속형+범주형|Log-Linear|
|Multinomial|Generalized Logit|연속형+범주형|Multinomial Response|
