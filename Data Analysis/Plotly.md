# Today I Learned - 2022/05/24

# Plotly

공식 문서 : https://plotly.com/python/time-series/

<br>

- 파이썬의 대표적인 인터랙티브 시각화 도구이다.
- conda 명령창을 통해 `conda install plotly` 명령어를 통해 설치한다.

```python
import plotly

plotly.__version__  # '5.8.0'
```

```python
import plotly.express as px

df = px.data.stocks()  # px 에서 내장하고 있는 data.stocks 데이터 load
```
<br>

- 날짜 데이터 타입인 date 컬럼을 인덱스로 설정한 후 모든 인덱스의 값을 -1 해준다.
- -1을 하여 기준을 0으로 만들어서 증가와 하락을 시각적으로 알아보기 쉽게 한다.
- 아래의 두 컬럼은 같은 결과를 나타낸다.

```python
df_1 = df.set_index("date") - 1
df_1 = px.data.stocks(indexed=True) - 1
```

```python
px.bar(df_1, x=df_1.index, y="GOOG")
```

```python
px.bar(df_1)  # 모든 컬럼에 대한 막대그래프 그리기
```
<br>

# facet_col을 이용한 서브플롯
- `px..area` : 분포를 그린다.
- `facet_col` : 서브플롯을 그려주는 기능을 한다.
<br>

주의 ❗ `facet_col`을 사용하려면 `df.columns.name`이 설정되어 있어야 한다.⭐
```python
df_1.columns  # Index(['GOOG', 'AAPL', 'AMZN', 'FB', 'NFLX', 'MSFT'], dtype='object')

df_1.columns.name = "company"
df_1.columns
# Index(['GOOG', 'AAPL', 'AMZN', 'FB', 'NFLX', 'MSFT'], dtype='object', name='company')
```

```python
px.area(df_1, facet_col="company")  # 아래 이미지는 area를 통해 분포를 그린 그래프이다.
px.bar(df_1, facet_col="company")
px.box(df_1, facet_col="company")
```
<br>

- `hover_data={"date": "|%Y-%m-%d"}`  : 시간을 표현한다.
```python
px.line(df, hover_data={"date" : "|%Y-%m-%d"} )
```
<br>

# Range Slider와 함께 시계열 그래프

- 그래프를 `fig` 라는 변수에 담아준다.
- `fig.update_xaxes(rangeslider_visible=True)` : Rangeslider를 볼 수 있다.

```python
fig = px.line(df_1, x=df_1.index, y="AAPL", title="AAPL주가")
fig.update_xaxes(rangeslider_visible=True)
fig.show()
```
<br>

# Candlestick
- 캔들스틱 차트(Candlestick chart) 또는 봉차트, 일본식 캔들스틱 차트는 주식을 비롯한 유가증권과 파생상품, 환율의 가격 움직임을 보여주는 금융 차트이다.
- 캔들스틱 차트는 기술 통계학에서 사용되는 상자 수염 그림과 외적으로 유사하지만, 상자 수염 그림은 캔들스틱과 달리 금융이 아닌 다른 정보들을 표시한다.
<br>

- fig.update_layout(xaxis_rangeslider_visible=True) : Rangeslider를 그린다.
- fig.update_layout(xaxis_rangeslider_visible=False) : Rangeslider를 그리지 않느다.
- True로 지정되거나 위 문구를 작성하지 않을 경우 Rangeslider가 포함된 그래프가 그려진다.

```python
import plotly.graph_objects as go

fig = go.Figure(data=[go.Candlestick(x=df['Date'],
                open=df['AAPL.Open'],
                high=df['AAPL.High'],
                low=df['AAPL.Low'],
                close=df['AAPL.Close'])])

fig.update_layout(xaxis_rangeslider_visible=False)  # 슬라이드 그리지 않음
fig.show()
```
<br>

# OHLC(Open-High-Low-Close)
- fig.update_layout(xaxis_rangeslider_visible=True) : Rangeslider를 그린다.
- fig.update_layout(xaxis_rangeslider_visible=False) : Rangeslider를 그리지 않느다.
- True로 지정되거나 위 문구를 작성하지 않을 경우 Rangeslider가 포함된 그래프가 그려진다.
```python
fig = go.Figure(data=[go.Ohlc(x=df['Date'],
                open=df['AAPL.Open'],
                high=df['AAPL.High'],
                low=df['AAPL.Low'],
                close=df['AAPL.Close'])])

fig.show()
```
<br>

# lineplot

```python
px.line(df_ratio)
px.line(df_ratio, facet_col="company")
```

# areaplot

```python
px.area(df_ratio)
px.area(df_ratio, facet_col="company")
px.line(tsla, x=tsla.index, y="Close", title="테슬라 종가")
```

# 막대그래프

```python
px.bar(df_ratio)
px.bar(df_ratio, facet_col="company")
```

# scatterplot

```python
px.scatter_matrix(df_ratio)
```

# distribution

## 1. box

- `points="all"` : 데이터 분포를 점으로 표현한다.
- `notched=True` : 그래프의 모습이 바뀐다. (default = True)

```python
px.box(df_ratio)
px.box(df_ratio, facet_col="company")
px.box(df_ratio, x="ZM")
px.box(df_ratio, x="ZM", points="all", notched=True)  # 아래 그래프에 해당
```

## 2. violin

- `points="all"` : 데이터 분포를 점으로 표현한다.
- `box=True` : violin 그래프 안에 boxplot을 그려준다.

```python
px.violin(df_ratio)
px.violin(df_ratio, facet_col="company")
```

## 3. strip

```python
px.strip(df_ratio)
px.strip(df_ratio, facet_col="company")
```

## 4. histogram

```python
px.histogram(df_ratio)
px.histogram(df_ratio, facet_col="company")
px.histogram(df_ratio, facet_col="company", marginal="box")
```

- `marginal` : box, violin 옵션을 주어 joint plot처럼 그릴 수 있다.
```python
px.histogram(tsla, x="Change", marginal="box")
px.histogram(tsla, x="Change", marginal="violin")
```
