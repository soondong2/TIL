# Today I Learned - 2022/09/14 Wed

# DataFrame

## csv 파일 불러오기
```r
df <- read.csv('파일명.csv', header=TRUE)
```
<br>

## 열 이름 변경
벡터 객체를 입력할 때는 `c()` 함수를 사용하여 결합시켜준다.
```r
# 열 이름 확인
names(df)

# 열 이름 변경
names(iris) <- c('sl', 'sw', 'pl', 'pw', 'sp')
```
<br>

## 특정 데이터만 추출
특정 데이터만 선택하여 추출하기 위해서는 `subset()` 함수를 사용한다.
```r
# sp 컬럼이 'versicolor'인 것만 추출
df1 <- subset(df, sp == 'versicolor')

# sl 컬럼이 6보다 크고, sp 컬럼이 'versicolor'인 것만 추출
df2 <- subset(df, sl > 6 & sp == 'versicolor')

#  sp 컬럼이 'setosa'인 sl, sw, sp 컬럼만 추출
df3 <- subset(df, sp == 'setosa', select=c(sl, sw, sp))

# select = -c(sp)은 데이터 셋에서 sp 컬럼만 제외하고 추출
df4 <- subset(df, select=-c(sp))
```
<br>

## 데이터 타입
```r
# 벡터
v <- c(1, 2, 3, 4, 5)

# 행렬
m <- matrix(c(1, 2, 3, 4, 5, 6, 7, 8, 9), nrow=3)

# 데이터 프레임
d <- data.frame(x=c(1, 2, 3), y=c(4, 5, 6), z=c('a', 'b', 'c'))

# 배열
a <- array(1:18, dim=c(2, 3, 3))

# 리스트
l <- list(name='J', family=c('S', 'T'))

# 데이터 타입 확인
class(v)
class(m)
class(d)
class(a)
class(l)
```
