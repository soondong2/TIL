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

<br>

## 23번

<br>

## 24번

<br>

## 25번

<br>
