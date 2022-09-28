# Today I Learned - 2022/09/28 Wed

# 상관분석(Correlation Analysis)
- 연속형인 두 변수 간에 어떤 선형적인 또는 비선형적인 관계를 갖고 있는지 분석하는 방법이다.
- 두 변수 간의 관계를 `상관계수(Correlation Coefficient)`로 나타낸다.
- 상관계수는 두 변수 간에 연관된 정도만을 나타낼 뿐, 인과관계를 설명하지는 않는다.
<br>

```r
# 데이터 불러오고 확인하기
df <- read.csv("ch5-1.csv", header=TRUE)
head(df)
str(df)

# 필요한 데이터만 담기
df1 <- df[, 2:5]

# 상관분석
corr <- cor(df1)
corr

# 산점도
plot(df1)

# 상관분석 결과를 corrplot 패키지로 그래프 그리기
install.packages("corrplot")
library(corrplot)
corrplot(corr)

# 원을 타원으로 표시하고, 하단에만 표시하고, 상관계수 표시
corrplot(corr, method="ellipse",
         type="lower",
         addCoef.col="white")
```
<br>

## corrplot
- `method` : circle, square, ellipse, number, pie
- `type` : 구역 표시로 full, lower, upper
- `addCoef.col` : 상관계수 색상 표시
- `title` : 제목 표시
