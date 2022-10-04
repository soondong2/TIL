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
