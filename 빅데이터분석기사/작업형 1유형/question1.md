# Today I Learned - 2022/06/03 Fri

## 1번
- 데이터셋(basic1.csv)의 `f5` 컬럼을 기준으로 상위 10개의 데이터를 구하고
- `f5`컬럼 10개 중 최소값으로 데이터를 대체한 후
- `age`컬럼에서 80 이상인 데이터의 `f5` 컬럼 평균값을 구하시오.

```python
import pandas as pd

basic = pd.read_csv("C:/data/basic1.csv")

basic = basic.sort_values(by="f5", ascending=False)
basic.iloc[:10, -1] = basic["f5"][:10].min()

result = basic[basic["age"] >= 80]["f5"].mean()
print(result)
```
62.49774712521738

<br>

## 2번
- 이상치(소수점 나이)를 찾고 올림, 내림, 버림(절사)한 후
- 3가지 모두 이상치 'age' 평균을 구한 다음 모두 더하여 출력하시오.
```python
import pandas as pd
import numpy as np

basic = pd.read_csv("C:/data/basic1.csv")

outlier = basic[(basic["age"] * 10) % 10 != 0]

outlier_ceil = np.ceil(outlier["age"]).mean()
outlier_floor = np.floor(outlier["age"]).mean()
outlier_trunc = np.trunc(outlier["age"]).mean()

result = outlier_ceil + outlier_floor + outlier_trunc
print(result)
```
69.5
