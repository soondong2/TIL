# Today I Learned - 2022/06/07 Tue

## 16번
- f1의 결측치를 채운 후 age 컬럼의 중복 제거 전과 후의 'f1' 중앙값 차이를 구하시오.

- 결측치는 f1의 데이터 중 내림차순 정렬 후 10번째 값으로 채움
- 중복 데이터 발생시 뒤에 나오는 데이터를 삭제함
- 최종 결과값은 절대값으로 출력
```python
import pandas as pd
import numpy as np

basic = pd.read_csv("C:/data/basic1.csv")

basic["f1"] = basic["f1"].fillna(basic.sort_values(by="f1", ascending=False).iloc[9, 3])
before_median = basic["f1"].median()

basic = basic.drop_duplicates(subset=['age'], keep="first")
after_median = basic["f1"].median()

result = abs(before_median - after_median)
print(result)
```
0.5

<br>

## 17번
- 새로운 컬럼(1일 이전 시차 컬럼)을 만들고
- Events가 1이면서 Sales가 1000000이하인 조건에 맞는 새로운 컬럼 합을 구하시오.
```oython
import pandas as pd
import numpy as np

basic = pd.read_csv("C:/data/basic2.csv", parse_dates=['Date'])

basic["prev_PV"] = basic['PV'].shift(1)
result = basic[(basic["Events"] == 1) & (basic["Sales"] <= 1000000)]["prev_PV"].sum()
print(result)
```
1894876.0

<br>

## 18번
- 데이터에서 IQR을 활용해 Fare컬럼의 이상치를 찾고
- 이상치 데이터의 여성 수를 구하시오.
```python
import pandas as pd

titanic = pd.read_csv('data/titanic.csv')

Q1 = titanic['Fare'].quantile(0.25)
Q3 = titanic['Fare'].quantile(0.75)
IQR = Q3 - Q1 

outlier = (titanic['Fare'] < (Q1 - 1.5 * IQR)) | ((Q3 + 1.5 * IQR) < titanic['Fare'])
titanic = titanic[outlier]

result = len(titanic[titanic['Sex'] == 'female'])
print(result)
```
70

<br>
