# Today I Learned - 2022/10/04 The

# 회귀분석(Regression Analysis)
- 연속형 변수들에 대해 두 변수 간의 관계를 수식으로 나타내는 분석 방법이다.
- x라는 독립변수와 y라는 종속변수가 존재할 때 두 변수 간의 관계를 **y = ax + b**와 같은 형태로 나타낼 수 있다.
<br>

## 회귀분석 가정
- `선형성` : 독립변수와 종속변수의 관계가 선형관계가 있다.
- `독립성` : 잔차와 독립변수의 값이 관련이 없어야 한다.
- `등분산성` : 독립변수의 모든 값에 대한 오차들의 분산이 일정해야 한다.
- `정상성` : 잔차항이 정규분포를 이뤄야 한다.
<br>

## 1. 단순 선형 회귀분석
- 종속변수와 독립변수가 각각 하나씩 존재하며 서로 선형적인 관계를 가질 때 사용하는 방법이다.
- y = ax + b 형태의 수식으로 나타낸다.
```r
df_lm <- lm(weight ~ egg_weight, data=df)
summary(df_lm)
```
```r
# 분석 결과
Call:
lm(formula = weight ~ egg_weight, data = df)

Residuals:
    Min      1Q  Median      3Q     Max 
-3.0177 -1.7148  0.1394  1.8080  2.9594 

Coefficients:
            Estimate Std. Error t value Pr(>|t|)    
(Intercept) -14.5475     8.7055  -1.671    0.106    
egg_weight    2.3371     0.1336  17.493   <2e-16 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 2.055 on 28 degrees of freedom
Multiple R-squared:  0.9162,	Adjusted R-squared:  0.9132 
F-statistic:   306 on 1 and 28 DF,  p-value: < 2.2e-16
```
<br>

1) 회귀모델이 통계적으로 유의한가? -> F통계량의 p-value < 2.2e-16 이므로 회귀모델이 유의하다.
2) 개별 독립변수가 통계적으로 유의한가? -> t통계량의 p-value < 2e-16 이므로 독립변수가 유의하다.
3) 모델의 설명력 -> 결정계수(R^2)가 0.9162 이므로 91.62% 설명력을 갖는다. 1에 가까울수록 좋다.
4) 추정 회귀식 -> weight = -14.5475 + 2.3371 * egg_ewight
<br>

### 산점도
- lm 모델에는 기본적으로 모델을 만들 때 사용한 독립변수를 이용해 종속변수를 맞춰본 값(fitted.values)이 들어있다.
- 객체의 이름은 `names()`를 통해 확인할 수 있다.
- 이외에도 `coefficients(계수)`, `residuals(잔차)`, 등 다양한 항목들이 존재한다.
```r
plot(df$egg_weight, df$weight)
lines(df$egg_weight, df_lm$fitted.values, col="blue")
text(x=66, y=132, label="Y = -14.5475 + 2.3371X")
```
<br>

### 잔차 그래프
```r
hist(df_lm$residuals, col="skyblue", xlab="residuals", main="제목")
```
<br>

## 2. 다중 회귀분석
- 독립변수가 2개 이상일 경우에 사용한다.
- y = ax1 + bx2 + c
```r
# 다중 회귀분석
df_mlm <- lm(weight ~ egg_weight + movement + food, data=df)
summary(df_mlm)
```
```r
# 결과
Call:
lm(formula = weight ~ egg_weight + movement + food, data = df)

Residuals:
    Min      1Q  Median      3Q     Max 
-3.2037 -1.3079  0.1826  1.2572  2.3647 

Coefficients:
             Estimate Std. Error t value Pr(>|t|)    
(Intercept)  2.974830   8.587203   0.346 0.731811    
egg_weight   1.776350   0.194845   9.117  1.4e-09 ***
movement    -0.008674   0.016631  -0.522 0.606417    
food         1.584729   0.404757   3.915 0.000583 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 1.681 on 26 degrees of freedom
Multiple R-squared:  0.9479,	Adjusted R-squared:  0.9419 
F-statistic: 157.7 on 3 and 26 DF,  p-value: < 2.2e-16
```
<br>

1) movement의 p-value가 0.606417로 통계적으로 유의하지 않다. -> 해당 독립변수는 회귀분석에서 제외 시킨다.
2) 수정된 결정계수가 0.9419 단순 회귀분석보다 높게 나타났다. -> movement 변수를 제외하고 다중 회귀분석을 실시하여 다시 평가한다.
<br>

```r
df_mlm2 <- lm(weight ~ egg_weight + food, data=df)
summary(df_mlm2)
```
```r
Call:
lm(formula = weight ~ egg_weight + food, data = df)

Residuals:
    Min      1Q  Median      3Q     Max 
-3.0231 -1.2124  0.2445  1.3607  2.2352 

Coefficients:
            Estimate Std. Error t value Pr(>|t|)    
(Intercept)   3.6638     8.3698   0.438 0.665052    
egg_weight    1.7453     0.1830   9.536 3.89e-10 ***
food          1.5955     0.3987   4.001 0.000441 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 1.658 on 27 degrees of freedom
Multiple R-squared:  0.9474,	Adjusted R-squared:  0.9435 
F-statistic:   243 on 2 and 27 DF,  p-value: < 2.2e-16
```
<br>

-> 수정된 결정계수(Adjusted R-squared)가 0.9435로 조금 더 높게 나타났다. 게다가 독립변수는 하나 더 줄어 회귀 모델은 간단해졌다.

<br>

## 3. 다중공선성
- 다중 회귀분석의 경우 단순 선형 회귀분석과 달리 독립변수가 많기 때문에 예상치 못한 독립변수들 간의 강한 상관관계로 인해 제대로 된 회귀분석이 실행되지 않을 수도 있다.
- `분산팽창요인(VIF)`을 계산해 구할 수 있는데 일반적으로 10 이상이면 다중공선성 문제가 있다고 판단하고, 30을 초과하면 심각한 문제가 있다고 판단한다.
- 분산팽창요인은 `car` 패키지를 이용하여 쉽게 구할 수 있다.

```r
# car 패키지
install.packages("car")
library(car)

# 다중공선성
vif(df_mlm2)

# 결과
egg_weight       food 
  2.882685   2.882685
```
<br>

1) 2가지 독립변수 모두 2.88 수준으로 10보다 작기 때문에 다중공선성 문제는 없는 것으로 판단된다.
2) 최종 회귀식은 weight = 3.6638 + 1.7453 * egg_weight + 1.599 * food 이다.
