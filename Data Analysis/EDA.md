# Today I Learned - 2022/05/25

# EDA

## Data Load
- `index_col=0` : 첫 번째 컬럼을 index로 설정, 컬럼명으로도 설정 가능
```python
pd.read_csv("파일 경로/파일명.csv")
pd.read_csv("파일 경로/파일명.csv", index_col=0)
```

## 중복값
```python
df[df.duplicated()]  # 중복값 확인
df.drop_duplicates()  # 중복값 제거
```

## Index
```python
df.set_index("column")
```

## 데이터 살펴보기
```python
df.shape
df.dtypes
df.columns
df.index
df.info()
df.isnull().sum()  # 결측치 개수
(df.isnull().sum() / df.shape[0]) * 100  # 결측치 비율
df.describe()
df.describe(include="object")
```

## 날짜 데이터
```python
pd.to_datetime(df["시계열 데이터"])

df["column"].dt.year  # 년
df["column"].dt.month  # 월
df["column"].dt.day  # 일
df["column"].dt.dayofweek  # 요일 (월 : 0 , ..., 일 : 7)
df["column"].dt.day_name()  # 요일(Monday, ..., Sunday)
```

## 빈도수
### 한 개의 변수에 대한 빈도수
```python
df["column"].value_counts()
```

### 두 개의 변수에 대한 빈도수
```python
pd.crosstab(df["column1"], df["column2"])  # 빈도수
pd.crosstab(df["column1"], df["column2"], normalize=True) * 100  # 빈도 비율
```

... ing
