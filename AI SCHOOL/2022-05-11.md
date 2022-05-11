# Today I Learned - 2022/05/11 Wed
---
## 📌 Pandas Profiling
```python
!pip install pandas-profiling==3.1.0

from pandas_profiling import ProfileReport
profile = ProfileReport(df, title="Pandas Profiling Report")

# 주피터 노트북이 있는 위치에 html파일이 생성된다.
profile.to_file("pandas_profile_report.html")
```

## 📌 sweetviz
- target 변수 없이 그릴 수도 있고, target 변수를 지정할 수도 있다.
- target 변수는 범주형이 아닌 `수치형` , `bool` 값만 가능하다.
- 데이터에 따라 수치형으로 되어 있지만 동작하지 않을 수도 있다.

```python
!pip install sweetviz

import sweetviz as sv

my_report = sv.analyze(df)
my_report = sv.analyze(df, target_feat ='target')
my_report.show_html()
```

## 📌 autoviz
```python
!pip install autoviz

from autoviz.AutoViz_Class import AutoViz_Class
AV = AutoViz_Class()

filename = "https://raw.githubusercontent.com/mwaskom/seaborn-data/master/mpg.csv"
sep = ","
dft = AV.AutoViz(
    filename,
    sep=",",
    depVar="",
    dfte=None,
    header=0,
    verbose=0,
    lowess=False,
    chart_format="html",
#     chart_format="bokeh",
    max_rows_analyzed=150000,
    max_cols_analyzed=30,
#     save_plot_dir=None
)
```
---
## 📌 수치형 데이터 시각화
### Import
```python
import pandas as pd
import numpy as np
import seaborn as sns
sns.set_style("whitegrid")
sns.set_context("talk")

import matplotlib.pyplot as plt
plt.style.use('seaborn')
```

- seaborn과 matplotlib에는 다양한 그래프 스타일 설정이 가능하다.
- seaborn의 그래프 스타일은 `darkgrid` , `whitegrid` , `dark` , `white` , `ticks` 5가지가 존재한다.
- 아래 코드를 통해 matplotlib의 그래프 종류가 어떤 것들이 있는지 알아볼 수 있다.
```python
plt.style.available
```

### 결측치 시각화
```python
sns.heatmap(df.isnull())
```

### 기술통계
```python
df.describe().style.background_gradient(cmap="Oranges") # default = blues
```

### 왜도
- 그래프의 좌우 비대칭 정도를 니티낸다.
- 왜도 > 0 : 오른쪽으로 긴 꼬리를 가진 분포이다.
- 왜도 = 0 : 정규분포이다.
- 왜도 < 0 : 왼쪽으로 긴 꼬리를 가진 분포이다.
```python
df.skew()
```

### 첨도
- 그래프의 봉우리가 뾰족한 정도를 나타낸다.
- 첨도 > 0 : 정규분포보다 뾰족한 봉우리를 가진 분포이다.
- 첨도 = 0 : 정규분포이다.
- 첨도 < 0 : 정규분포보다 완만한 봉우리를 가진 분포이다.
```python
df.kurt()
```

```python
df["mpg"].agg(["skew", "kurt", "mean", "median"])
```

### 히스토그램
모든 변수에 대해 히스토그램을 그린다.

```python
df.hist(figsize=(10, 10), bins=10)
plt.show()
```

```python
sns.kdeplot(data=df, x="column")
sns.displot(data=df, x="column", kde=True)  # 히스토그램 + kde
```

```python
sns.kdeplot(data=df, x="column", shade=True)
sns.rugplot(data=df, x="column")
```

### 잔차 시각화
```python
sns.residplot(data=df, x="column1", y="column2")
```

### 서브플롯
```python
sns.lmplot(data=df, x="num_column1", y="num_column2", hue="cat_column", col="cat_column")
```

### Jointplot
- kind = ["kde", "scatter", "hist", "hex"]
```python
sns.jointplot(data=df, x="column", y="column", kind="scatter")
```

### pairplot
```python
sns.pairplot(data=df, hue="cat_column")
```

### lineplot
```python
sns.lineplot(data=df, y="column", x="column")
```

### regplot
- col="origin” : origin별로 서브플롯을 그려준다.
```python
sns.relplot(data=df, x="column1", y="column2", hue="cat_column", kind="line")
```

### 히트맵
```python
mask = np.triu(np.ones_like(corr))
mask
```
```
[[1., 1., 1., 1., 1., 1., 1.],
 [0., 1., 1., 1., 1., 1., 1.],
 [0., 0., 1., 1., 1., 1., 1.],
 [0., 0., 0., 1., 1., 1., 1.],
 [0., 0., 0., 0., 1., 1., 1.],
 [0., 0., 0., 0., 0., 1., 1.],
 [0., 0., 0., 0., 0., 0., 1.]]
```

```python
sns.heatmap(corr, annot=True, cmap="coolwarm", mask=mask, vmin=-1, vmax=1)
```

- `annot=True` : 상관계수를 그래프에 나타낸다.
- `vmin=-1`, `vmax=1` : 가장 작은 값과 가장 큰 값의 색상을 강조한다.
- `cmap` : 그래프 색상을 나타낸다.

```python
print(plt.colormaps()) # cmap으로 가능한 색상들을 보여준다.
```

---

## 📌 범주형 데이터 시각화
### countplot
```python
sns.countplot(data=df, x="cat_column")
sns.countplot(data=df, hue="cat_column1", x="cat_column2")
```

### crosstap
```python
pd.crosstab(index=df["cat_column"], columns=df["cat_column"])
```

### 빈도수
```python
df["column"].value_counts()
```
