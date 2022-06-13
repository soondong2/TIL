# Today I Learned - 2022/06/13 Mon

## 26번
- 데이터셋(basic1.csv)의 앞에서 순서대로 `70%` 데이터만 활용해서
- `f1`컬럼 결측치를 중앙값으로 채우기 전후의 `표준편차`를 구하고 두 표준편차 차이 계산하시오.
```python
import pandas as pd
import numpy as np
from sklearn.preprocessing import MinMaxScaler

basic = pd.read_csv("C:/data/basic1.csv")

basic = basic.iloc[:int(basic.shape[0] * 0.7), :]

before = basic["f1"].std() 
basic["f1"] = basic["f1"].fillna(basic["f1"].median())
after = basic["f1"].std()

result = abs(before - after)
print(result)
```
3.2965018033960725

<br>

## 27번
- 데이터셋(basic1.csv)의 `age`컬럼의 `이상치`를 더하시오.
- 단, 평균으로부터 `표준편차x1.5`를 벗어나는 영역을 이상치라고 판단함
```python
import pandas as pd
import numpy as np
from sklearn.preprocessing import MinMaxScaler

basic = pd.read_csv("C:/data/basic1.csv")

outlier = ((basic["age"].mean() - 1.5 * basic["age"].std()) > basic["age"]) | (basic["age"] >(basic["age"].mean() + 1.5 * basic["age"].std()))

result = basic[outlier]["age"].sum()
print(result)
```
473.5

<br>

## 28번

## 29번

## 30번

## 31번
