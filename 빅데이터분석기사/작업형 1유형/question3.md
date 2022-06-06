# Today I Learned - 2022/06/06 Mon

## 11번
- 주어진 데이터에서 `2022`년 `5월` `주말`과 `평일`의 `sales`컬럼 평균값 차이를 구하시오.
- 소수점 둘째자리까지 반올림
```python
import pandas as pd
import numpy as np

basic = pd.read_csv("C:/data/basic2.csv")

basic = basic[basic["Date"].str.contains("2022-05")]
basic["Date"] = pd.to_datetime(basic["Date"])
basic["Weekday"] = basic["Date"].dt.day_name()

weekend = basic[(basic["Weekday"] == "Saturday") | (basic["Weekday"] == "Sunday")]["Sales"].mean()
weekday = basic[~((basic["Weekday"] == "Saturday") | (basic["Weekday"] == "Sunday"))]["Sales"].mean()

result = round(abs(weekend - weekday), 2)
print(result)
```
3010339.1

<br>

## 12번
- `2022`년 월별 Sales 합계 중 가장 큰 금액과 `2023`년 월별 Sales 합계 중 가장 큰 금액의 차이를 절대값으로 구하시오.
- 단 `Events`컬럼이 `1`인경우 80%의 Salse값만 반영한다. (최종값은 소수점 반올림 후 정수 출력)
```python
import pandas as pd
import numpy as np

basic = pd.read_csv("C:/data/basic2.csv")

basic["Date"] = pd.to_datetime(basic["Date"])
basic["Year"] = basic["Date"].dt.year
basic["Month"] = basic["Date"].dt.month

def event(x):
    if x['Events'] == 1:
        x['Sales2'] = x['Sales'] * 0.8
    else:
        x['Sales2'] = x['Sales']
    return x

basic = basic.apply(lambda x: event(x), axis=1)

max_2022 = basic[basic["Year"] == 2022].groupby(["Month"])[["Sales2"]].sum().max()
max_2023 = basic[basic["Year"] == 2023].groupby(["Month"])[["Sales2"]].sum().max()

result = int(abs(max_2022 - max_2023))
print(result)
```
42473435

<br>

## 13번
- basic1 데이터 중 `f4`를 기준으로 basic3 데이터 `f4`값을 기준으로 병합하고
- 병합한 데이터에서 r2결측치를 제거한 다음
- 앞에서 부터 20개 데이터를 선택하고 'f2'컬럼 합을 구하시오.

- basic1.csv: 고객 데이터
- basic3.csv: 잘 어울리는 관계 데이터 (추천1:r1, 추천2:r2)
```python
import pandas as pd
import numpy as np

basic1 = pd.read_csv("C:/data/basic1.csv")
basic3 = pd.read_csv("C:/data/basic3.csv")

basic = pd.merge(basic1, basic3, on="f4", how="left")
# basic.isnull().sum()
basic = basic.dropna(subset="r2").head(20)

result = basic["f2"].sum()
print(result)
```
15

<br>

## 14번
- basic1 데이터 중 `age`컬럼 `이상치`를 제거하고
- 동일한 개수로 나이 순으로 3그룹으로 나눈 뒤 각 그룹의 중앙값을 더하시오. (이상치는 음수, 0, 소수점 값)
```python
import pandas as pd
import numpy as np

basic = pd.read_csv("C:/data/basic1.csv")

basic = basic[~((basic["age"] <= 0) | (basic["age"] * 10) % 10 != 0)]
basic["range"] = pd.qcut(basic["age"], 3, labels=["group1", "group2", "group3"])

result = basic.groupby(["range"])["age"].median().sum()
print(result)
```
165.0
<br>

## 15번
- `주` 단위 `Sales`의 합계를 구하고
- 가장 큰 값을 가진 주와 작은 값을 가진 주의 `절댓값 차이`를 구하시오.
```python
import pandas as pd
import numpy as np

basic = pd.read_csv("C:/data/basic2.csv", parse_dates=['Date'], index_col=0)
max_sales = basic['Sales'].resample('W').sum().min()
min_sales = basic['Sales'].resample('W').sum().max()

result = abs(max_sales - min_sales)
print(result)
```
91639050
