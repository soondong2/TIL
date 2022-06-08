# Today I Learned - 2022/06/08 Wed

# Downcast

## Data Load

```python
import pandas as pd

df = pd.read_csv("C:/Users/user/Desktop/data/Lion/nhis_drug_sample_2020_3.csv")
```

```python
df.info()  # 36.4 MB
```

<br>

## Data type에 대한 데이터 크기
## downcast
- Shift + Tap 도움말을 통해 확인한다.
- downcast=None이 기본값이며 `signed` 또는 `intege` , `unsigned` , `float` 등 옵션이 있다.
- 아래의 방법은 하나의 컬럼의 dtype을 변경하는 방법이다.
```python
df["성별코드"]
df["성별코드"] = pd.to_numeric(df["성별코드"], downcast="unsigned")
```

<br>

> downcast 방법
- `bool` → `int8` (음수 O)
- `int` →  `unsigned` (음수 X)
- `float` →  `float`
```python
1. df[col].dtype.name 으로 데이터 타입명을 가져온다.
2. 각 컬럼의 데이터 타입 이름이 `int`,  `float` 으로 시작하는지를 확인한다.
3. downcast 는 pd.to_numeric를 사용하여 변경한다.
```

<br>

- 반복문, 조건문
```python
for col in df.columns:
    dtype_name = df[col].dtypes.name
    if dtype_name.startswith("int"):
        df[col] = pd.to_numeric(df[col], downcast="unsigned")
    elif dtype_name.startswith("float"):
        df[col] = pd.to_numeric(df[col], downcast="float")
    elif dtype_name == "bool":
        df[col] = df[col].astype("int8")
```

<br>

- df.select_dtypes
```python
fcols = df.select_dtypes('float').columns
icols = df.select_dtypes('integer').columns
bcols = df.select_dtypes('bool').columns

df[fcols] = df[fcols].apply(pd.to_numeric, downcast='float')
df[icols] = df[icols].apply(pd.to_numeric, downcast='unsigned')
df[bcols] = df[bcols].apply(pd.to_numeric, downcast='int8')
```

<br>

- object 타입 변경
```python
scols = df.select_dtypes('object').columns 
df[scols] = df[scols].astype('category')
```

<br>
⇒  downcast를 하기 전 `36.4 MB`에서 downcast를 한 후에 `10.4MB`로 줄어들었다.
