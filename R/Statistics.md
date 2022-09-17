# Today I Learned - 2022/09/15 Thur

# 기초 통계량
## 데이터 확인
```r
head(df)  # 처음부터 6행까지
tail(df)  # 마지막부터 6행까지
```
<br>

## 기초 통계량
```r
sum(df$chick)  # 합계
mean(df$chick)  # 평균
sd(df$chick)  # 표준편차
median(df$chick)  # 중앙값
min(df$chick)  # 최소값
max(df$chick)  # 최대값
```
<br>

## 데이터 정렬
```r
df[order(df$chick), ]  # 오름차순 정렬
df[order(-df$chick), ]  # 내림차순 정렬
```
<br>
