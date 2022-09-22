# Today I Learned - 2022/09/21 Wed

# 그래프
## 막대그래프
|함수|설명|
|:---:|:---:|
|names.arg|가로축의 항목 이름 표시|
|col|막대 색상, 항목 여러 개일 경우 c() 함수 이용|
|main|그래프 제목 표시|
|xlab|x축 이름|
|ylab|y축 이름|
|ylim|y축 상한값, 하한값|

<br>

```r
# 기본 막대그래프
barplot(df$column)

# 옵션
barplot(df$y_column, names.arg=df$x_column,
        col=c("red", "orange", "yellow", "green", "blue", "navy", "violet"),
        main="제목", xlab="x축", ylab="y축",
        ylim=c(0, 35))
```
<br>

## 그래프 색상
```r
install.packages("RColorBrewer")  # 색상 팔레트 패키지 설치
library(RColorBrewer)

display.brewer.all()  # 색상 팔레트 확인
```
<br>

```r
color <- brewer.pal(7, "Pastel2")  # Pastel2 팔레트에서 7개의 색상 가져옴
barplot(df$y_column, names.arg=df$x_column,
        col=color,
        main="제목", xlab="x축", ylab="y축",
        ylim=c(0, 35))
```
<br>

## 그래프 위에 텍스트 추가
- R에서는 텍스트나 선을 표시하기 위해 `text()`와 `abline()` 함수를 이용한다.
- 막대그래프에서 각 막대의 x 좌표를 구하는 방법 (x 좌표 이름이 범주형으로 되어 있을 경우)
- `pos` : 좌표를 나타낸다. 1(아래), 2(왼쪽), 3(위), 4(오른쪽)
```r
bar_x <- barplot(df$chick)  # barplot으로 그린 x 좌표 집어넣기

barplot(df$y_column, names.arg=df$x_column, col=color,
        main="제목", xlab="x축", ylab="y축", ylim=c(0, 35))
text(x=bar_x, y=df$y_column, labels=df$y_column, pos=3)  # 텍스트 추가
```
<br>

## 그래프 위에 선 추가
- `abline()` 함수를 이용해 점선을 그린다.
- `lty` : 선의 모양
- `lwd` : 선의 굵기
```r
abline(h=30, col="red", lty=2, lwd=1)  # y값 30을 기준으로 점선 표시
```
<br>

## 파이 차트
- 파이 차트는 주로 전체에서 항목별 비율을 확인할 때 사용한다.
- `pie()` 함수를 통해 파이 차트를 그릴 수 있다.
- `paste()` 함수는 텍스트로 여러 항목을 보여주고자할 때 사용한다.
```r
df$pct <- round(df$chick / sum(df$chick) * 100, 1)  # 비율 구하기

pie(df$chick, labels=paste(df$hatchery, df$pct, "%"),
    col=color, clockwise=TRUE, main="비율")
```
