# Today I Learned - 2022-06-05 Sun

## 6번
- 주어진 데이터에서 상관관계를 구하고
- `quality`와의 상관관계가 가장 큰 값과, 가장 작은 값을 구한 다음 더하시오.
- 단, quality와 quality 상관관계 제외, 소수점 둘째 자리까지 출력
```python
import pandas as pd
import numpy as np

wine = pd.read_csv("C:/data/winequality.csv")

corr = abs(wine.corr()[["quality"]].iloc[:-1]).sort_values(by="quality", ascending=False)
corr_max = corr.iloc[0]
corr_min = corr.iloc[-1]

result = round(corr_max + corr_min, 2).values[0]
print(result)
```
0.49

<br>

## 7번
- `city`와 `f4`를 기준으로 `f5`의 `평균값`을 구한 다음
- f5를 기준으로 상위 7개 값을 모두 더해 출력하시오 (소수점 둘째자리까지 출력)
```python
import pandas as pd
import numpy as np

basic = pd.read_csv("C:/data/basic1.csv")

result = round(basic.groupby(["city", "f4"])[["f5"]].mean().sort_values(by="f5", ascending=False).head(7).sum().values[0], 2)
print(result)
```
643.68

<br>

## 8번
- 주어진 데이터 셋에서 `age`컬럼 상위 `20개`의 데이터를 구한 다음
- `f1`의 결측치를 `중앙값`으로 채운다.
- `f4`가 `ISFJ`와 `f5`가 20 이상인 `f1`의 `평균값`을 출력하시오.
```python
import pandas as pd
import numpy as np

basic = pd.read_csv("C:/data/basic1.csv")

basic = basic.sort_values(by="age", ascending=False).head(20)
basic["f1"] = basic["f1"].fillna(basic["f1"].median())

result = basic[(basic["f4"] == "ISFJ") & (basic["f5"] >= 20)]["f1"].mean()
print(result)
```
73.875

<br>

## 9번
- 주어진 데이터 셋에서 `f2`가 `0`값인 데이터를 `age`를 기준으로 `오름차순` 정렬하고
- 앞에서 부터 20개의 데이터를 추출한 후
- `f1` 결측치(최소값)를 채우기 전과 후의 `분산 차이`를 계산하시오 (소수점 둘째 자리까지)
```python
import pandas as pd
import numpy as np

basic = pd.read_csv("C:/data/basic1.csv")

basic = basic[basic["f2"] == 0].sort_values(by="age", ascending=True).head(20)
before_var = basic["f1"].var() 

basic["f1"] = basic["f1"].fillna(basic["f1"].min())
after_var = basic["f1"].var()

result = round(abs(before_var - after_var), 2)
print(result)
```
38.44

<br>

## 10번
- 2022년 5월 sales의 중앙값을 구하시오.
<br>

💻 Datetime을 이용한 방법
```python
import pandas as pd
import numpy as np

basic = pd.read_csv("C:/Users/user/Desktop/data/basic2.csv")

basic["Date"] = pd.to_datetime(basic["Date"])
basic["Year"] = basic["Date"].dt.year
basic["Month"] = basic["Date"].dt.month

result = basic[(basic["Year"] == 2022) & (basic["Month"] == 5)]["Sales"].median()
print(result)
```
<br>

💻 str.contains를 이용한 방법
```python
import pandas as pd
import numpy as np

basic = pd.read_csv("C:/Users/user/Desktop/data/basic2.csv")

result = basic[basic["Date"].str.contains("2022-05")]["Sales"].median()
print(result)
```
1477685.0
