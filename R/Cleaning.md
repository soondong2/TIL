# Today I Learned - 2022/09/15 Thur

# 데이터 정제

## 결측치(NA)
### 결측치 제외
`na.omit()` 함수를 이용하여 결측치를 제외한 데이터 확인
```r
na.omit(df)
```
<br>

### 중앙값으로 대체
- 극단값이 존재할 경우 평균을 대표값으로 사용할 때 왜곡이 발생될 수 있으므로 중앙값을 사용한다
- 결측치를 중앙값으로 대체하기 위해서는 `DMwR2` 라는 패키지를 설치하여 사용한다.
```r
# 패키지 설치 및 불러오기
install.packages("DMwR2")
library(DMwR2)

# 결측치 대체
median(df$PM10, na.rm=TRUE)  # 결측치를 제외한 중앙값
median(df$PM25, na.rm=TRUE)  # 결측치를 제외한 중앙값

df2 <- centralImputation(df)  # 결측치 대체

df[14:16, ]  # 결측치 대체 전
df2[14:16, ]  # 결측치 대체 후
```
<br>

### 인접값 가중 평균으로 대체(K-NN)
`knnImputation()` 함수를 이용해 K-NN 알고리즘을 이용하여 결측치를 대체한다.
```r
df3 <- df[, -1]  # 첫 번째 열을 제외하고 별도의 데이터 

df4 <- knnImputation(df3)  # 결측치 대체

df4[14:16, -1]  # 결측치 대체 후
```
