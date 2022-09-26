# Today I Learned - 2022/09/26 Mon

# 정규분포와 중심극한 정리
```r
df <- read.csv("data.csv", header=TRUE)
summary(df)  # 주요 통계량
```

## 히스토그램
- 대이터의 분포를 확인할 때 사용하는 가장 대표적인 그래프이다.
- 데이터가 적당히 많을 경우(30건 이상) 정규분포에 가까운 분포를 띈다. -> `중심극한정리`
- 평균과 표준편차만 알고 있어도 대략적인 데이터의 분포를 알아낼 수 있다.
```r
hist(df$column, col="sky blue", xlab="x 축 이름", main="제목")
```
<br>

## 상자그림
- 1사분위수, 3사분위수, 중앙값, 최소값, 최대값, 이상치를 확인해볼 수 있다.
- 히스토그램과 마찬가지로 데이터의 분포를 확인할 때 사용한다.
```r
boxplot(df$column, col="sky blue", main="제목")
```
<br>

## 다중 그래프
- 그래프를 한 번에 2개 이상 그리기 위해서는 `par()` 함수를 이용한다.
- `mfrow` 옵션은 그래프의 배치를 정하는데 사용하며 `c(행 개수, 열 개수)`를 입력한다.
```r
par(mfrow=c(2, 1))

hist(df$column, col="sky blue", xlab="x 축 이름", main="제목")
boxplot(df$column, col="sky blue", main="제목")
```
