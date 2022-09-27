# Today I Learned - 2022/09/27 Tue

# 가설검정(Hypothesis Test)
가설검정이란 추론통계의 영역으로 '비교하는 값과 차이가 없다'는 가정의 귀무가설과 반대인 대립가설을 설정해 검정 통계량으로 가설의 진위를 판단하는 방법이다.
<br>
<br>

## 정규분포인지 검정
- 두 집단 간의 평균이 같은지 다른지 가설검정 하기 위해 `t-test`를 진행한다.
- t-test는 데이터가 **정규분포**를 따른다는 가정하에 평균이 데이터의 대표값 역할을 한다고 전제한다.
- t-test를 수행하기 전에 데이터가 정규분포를 따르는지 `Shapiro-Wilk` 검정을 통해 판정한다.
<br>

- `subset()` 함수는 데이터 셋에서 필요한 데이터만 필터링하여 다른 데이터 셋을 만들어준다.
- `shapiro.test()` 함수를 통해 샤피로-윌크 검정을 진행한다.
```r
# subset 함수를 통해 조건에 해당하는 데이터프레임 추출
a <- subset(df$weight, df$hatchery=="A")
b <- subset(df$weight, df$hatchery=="B")

# 샤피로-윌크 검정
shapiro.test(a)
shapiro.test(b)
```
<br>

- 샤피로-윌크 검정 결과
```r
shapiro.test(a)

	Shapiro-Wilk normality test

data:  a
W = 0.94, p-value = 0.553


shapiro.test(b)

	Shapiro-Wilk normality test

data:  b
W = 0.93907, p-value = 0.5427
```
-> a, b 데이터 셋의 p-value가 0.553, 0.5427으로 유의하지 않기 때문에 귀무가설을 기각할 수 없다. 따라서 두 데이터 셋 모두 정규분포를 따른다.
<br>

## t-test로 두 집단 간 평균 검정
- `t.test()` 함수를 통해 t-test 평균 검정을 진행한다.
```r
t.test(data=df, weight ~ hatchery)
```
```r
	Welch Two Sample t-test

data:  weight by hatchery
t = 2.8425, df = 17.673, p-value = 0.01094
alternative hypothesis: true difference in means between group A and group B is not equal to 0
95 percent confidence interval:
  1.71544 11.48456
sample estimates:
mean in group A mean in group B 
          110.8           104.2
```
-> p-value가 0.01094로 유의수준 0.05보다 작기 때문에 귀무가설을 기각한다. 즉 두 집단의 평균은 서로 다르다.
