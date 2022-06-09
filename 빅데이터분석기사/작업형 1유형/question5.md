# Today I Learned - 2022/06/08 Wed

## 21번
- 주어진 데이터에서 `f5`컬럼을 `표준화`(Standardization (Z-score Normalization))하고
- `중앙값`을 구하시오.
```python
import pandas as pd
import numpy as np
from sklearn.preprocessing import StandardScaler

basic = pd.read_csv("C:/data/basic1.csv")

scale = StandardScaler()
basic["f5"] = scale.fit_transform(basic[["f5"]])

result = basic["f5"].median()
print(result)
```
0.260619629559015

<br>

## 22번
- 주어진 데이터에서 `20세 이상`인 데이터를 추출하고
- `f1` 컬럼을 결측치를 최빈값으로 채운 후
- `f1` 컬럼의 `여-존슨`과 `박스콕스` 변환 값을 구하고
- 두 값의 차이를 `절대값`으로 구한다음 모두 더해 소수점 둘째 자리까지 출력(반올림)하시오.
```python
import pandas as pd
import numpy as np
from sklearn.preprocessing import power_transform

basic = pd.read_csv("C:/data/basic1.csv")

basic = basic[basic["age"] >= 20]
f1_mode = basic["f1"].value_counts(ascending=False).index[0]
basic["f1"] = basic["f1"].fillna(f1_mode)

basic["yeo"] = power_transform(basic[["f1"]], standardize=False)
basic["boxcox"] = power_transform(basic[["f1"]], method="box-cox", standardize=False)

result = round(abs(basic["yeo"] - basic["boxcox"]).sum(), 2)
print(result)
```
39.17

<br>

## 23번
- 주어진 데이터에서 `f5` 컬럼을 `min-max` 스케일 변환한 후
- `상위 5%`와 `하위 5%` 값의 `합`을 구하시오.
```python
import pandas as pd
import numpy as np
from sklearn.preprocessing import MinMaxScaler

basic = pd.read_csv("C:/data/basic1.csv")

scale = MinMaxScaler()
basic["f5"] = scale.fit_transform(basic[["f5"]])

result = basic["f5"].quantile(0.05) + basic["f5"].quantile(0.95)
print(result)
```
1.0248740983597389

<br>

## 24번
- 주어진 데이터에서 `상위 10개` 국가의 접종률 평균과 `하위 10개` 국가의 접종률 `평균`을 구하고
- 그 차이를 구해보시오. (단, 100%가 넘는 접종률 제거, 소수 첫째자리까지 출력)
```python
import pandas as pd

covid = pd.read_csv("C:/data/covid-vaccination-vs-death_ratio.csv", index_col=0)

covid = covid.groupby('country').max()
covid = covid.sort_values('ratio', ascending=False)
covid = covid[~(covid['ratio'] >= 100)]

top = covid['ratio'].head(10).mean()
bottom = covid['ratio'].tail(10).mean()

result = round(top - bottom, 1)
print(result)
```
87.8

<br>

## 25번

<br>
