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
- `age`의 이상치(소수점 나이)를 찾고 `올림`, `내림`, `버림`(절사)한 후
- 3가지 모두 이상치 `age` 평균을 구한 다음 모두 더하여 출력하시오.
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

<br>

## 3번
- 주어진 데이터에서 결측치가 80%이상 되는 컬럼은 삭제하고
- 80% 미만인 결측치가 있는 컬럼은 `city`별 `중앙값`으로 값을 대체하고
- `f1`컬럼의 `평균값`을 출력하시오.
```python
import pandas as pd
import numpy as np

basic = pd.read_csv("C:/data/basic1.csv")

(basic.isnull().sum() / basic.shape[0]) * 100
basic = basic.drop(["f3"], axis=1)

city_dict = {}
for i, city in enumerate(basic.groupby(["city"])["f1"].median().index.tolist()):
    city_dict[city] = basic.groupby(["city"])["f1"].median().tolist()[i]

basic["f1"] = basic["f1"].fillna(basic["city"].map(city_dict))

result = basic["f1"].mean()
print(result)
```
65.52

<br>

## 4번
- 주어진 데이터 중 train.csv에서 `SalePrice`컬럼의 `왜도`와 `첨도`를 구한 값과,
- `SalePrice`컬럼을 스케일링(`log1p`)로 변환한 이후
- 왜도와 첨도를 구해 모두 더한 다음 소수점 2째자리까지 출력하시오.
```python
import pandas as pd
import numpy as np

train = pd.read_csv("C:/Users/user/Desktop/data/train.csv")

prev_skew = train["SalePrice"].skew()
prev_kurt = train["SalePrice"].kurt()

train["SalePrice"] = np.log1p(train["SalePrice"])

after_skew = train["SalePrice"].skew()
after_kurt = train["SalePrice"].kurt()

result = prev_skew + prev_kurt + after_skew + after_kurt
print(round(result, 2))
```
9.35

<br>

## 5번
- 주어진 데이터 중 basic1.csv에서 `f1`컬럼 결측 데이터를 제거하고
- `city`와 `f2`을 기준으로 묶어 합계를 구하고
- `city`가 경기이면서 `f2`가 `0`인 조건에 만족하는 `f1` 값을 구하시오.
```python
import pandas as pd
import numpy as np

basic = pd.read_csv("C:/data/basic1.csv")

basic = basic[~basic["f1"].isnull()]
basic = basic.groupby(["city", "f2"], as_index=False)[["f1"]].sum()

result = basic[(basic["city"] == "경기") & (basic["f2"] == 0)]["f1"].values[0]
print(result)
```
833.0

<br>

