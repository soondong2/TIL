# Today I Learned - 2022/05/11 Wed

## Pandas Profiling

```python
!pip install pandas-profiling==3.1.0

from pandas_profiling import ProfileReport
profile = ProfileReport(df, title="Pandas Profiling Report")

# 주피터 노트북이 있는 위치에 html파일이 생성된다.
profile.to_file("pandas_profile_report.html")
```

## sweetviz

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

## autoviz

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

- 위 방법들은 짧은 코드로 모든 변수들의 기술통계와 시각화를 보여준다.
- 비교적 편리하다는 장점은 있으나, 변수 개수가 많을 경우 시간이 오래 걸리거나 작동하지 않을 수도 있으며, 자유롭게 원하는 변수만들 선택하여 비교하긴 어렵다는 단점이 있다.
