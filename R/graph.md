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
barplot(df$chick, names.arg=df$hatchery,
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
barplot(df$chick, names.arg=df$hatchery,
        col=color,
        main="제목", xlab="x축", ylab="y축",
        ylim=c(0, 35))
```
<br>

## 텍스트 추가
- R에서는 텍스트나 선을 표시하기 위해 `text()`와 `abline()` 함수를 이용한다.
