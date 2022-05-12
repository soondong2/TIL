# Today I Learned - 2022/05/10 Tue
---
## 📌 Pandas
```python
import pandas as pd
import numpy as np
```
- Pandas에는 `DataFrame` 형태와 `Series` 형태가 존재한다.
- `DataFrame` 은 2차원 형태, `Series` 는 1차원 벡터이다.

## 📌 DataFrame
### 데이터프레임 생성
```python
df = pd.DataFrmae()
```

### 데이터프레임에 컬럼 추가
```python
df["column"] = 단일 값
df["column"] = ["A", "B", ..., "Z"]
df["column"] = [1, 2, ..., 10]
```

### 컬럼의 값들을 리스트 형태로 변환
```python
df["column"].tolist()
```

### 컬럼 삭제
```python
df.drop(["column"], axis=0)  # axis=0 : 행(index)
df.drop(["column"], axis=1)  # axis=1 : 열(columns)
df.drop(["column1", "column2", ...], axis=1)  # 한 번에 여러 개도 삭제 가능
```

### 데이터 살펴보기
```python
df.info()  # 정보
df.shape  # 크기 (행, 열)
df.head()  # 앞에서 5개만 보기(default=5 이지만 원하는 숫자 지정 가능)
df.tail()  # 뒤에서 5개만 보기(default=5 이지만 원하는 숫자 지정 가능)
df.describe()  # 기술통계량 (수치형 데이터)
df.describe(include="object")  # 기술통계량 (범주형 데이터)
df.unique()  # 유일값
df.nunique()  # 유일값의 개수
df.dtypes  # 컬럼의 타입
df.index  # 인덱스
df.columns  # 컬럼만 보기
df.values  # 값만 보기
df.sample()  # Random한 값을 1개 반환
df.sample(5)  # Random한 값을 5개 반환
df.sample(frac=0.1, random_state=42)  # 10%의 값을 반환

# random_state : 난수 고정
```

### 데이터 가져오기
- ⭐ 두 개 이상의 컬럼명을 가져올 때는 `[]` 가 아닌 `[[]]` 대괄호 두 개를 사용한다 .
- ⭐ `df["column"]` 은 `Series` 형태로 반환하고, `df[["column"]]` 은 `DataFrame` 형태로 반환한다 .

```python
df["column"]
df[["column1", "column2"]]
```

### .loc 와 .iloc
- ⭐ `df.loc` 는 index의 이름으로 값을 가져오고, `df.iloc` 는 index의 위치로 값을 가져온다 .
- ⭐ 인덱싱과 슬라이싱이 가능하다 .

```python
df.loc[행, 열]
df.loc[[행1, 행2], [열1, 열2]]

df.iloc[행, 열]
df.loc[[행1, 행2], [열1, 열2]]
```

💡 `%timeit` 을 실행하려는 코드 앞에 입력해주면 코드 실행 소요 시간이 나타난다.

### str
```python
df.str.contains("A|B")  # df에 "A" 또는 "B"가 포함된 값들을 불린 값으로 반환
df.str.lower()  # 모두 소문자로 변경
df.str.upper()  # 모두 대문자로 변경
```

### 정렬
```python
df.sort_values(by="column", ascending=True)  # "column"을 기준으로 오름차순 정렬
df.sort_values(by="column", ascending=True)  # "column"을 기준으로 내림차순 정렬

df.sort_values(by=["column1", "column2"], ascending=True)  # column1로 정렬 후 column2 로 정렬

df["column"].sort_values(ascending=False)
```

### csv 파일로 저장
```python
df.to_csv("파일명.csv", index=False)
```

- csv 파일 불러오기
```python
pd.read_csv("파일 경로/파일명.csv")
pd.read_csv("파일 경로/파일명.csv", index_col=0)  # 첫 번째 컬럼을 index로 지정
```

### 상관계수
- ⭐ -1 ≤ r ≤ 1  : 상관계수(r)은 -1에서 1까지의 값을 갖는다.
- ⭐ 양의 상관계수 : 양의 상관관계가 존재한다. 한 변수가 증가함에 따라 다른 변수도 증가한다.
- ⭐ 음의 상관계수 : 음의 상관관계가 존재한다. 한 변수가 증가함에 따라 다른 변수는 감소한다.
- ⭐ 0 : 상관관계가 존재하지 않는다.

```python
df.corr()
```

### 빈도수
```python
df["column"].value_counts()
df["column"].value_counts(normalize=True)
```

### groupby
```python
df.groupby(["column"]).mean()
df.groupby(["column"]).sum()
df.groupby(["column"]).describe()
```
---
## 📌 Seaborn
matplotlib을 추상화 해놓은 시각화 도구이다.

### countplot
```python
sns.countplot(data=df, x="cat_column")  # 세로 축
sns.countplot(data=df, y="cat_column")  # 가로 축
```

### barplot
```python
# 기본값 : 평균
sns.barplot(data=df, x='cat_column', y="column")

# sd : 표준편차
sns.barplot(data=df, x='cat_column', y="column", ci="sd")
```

### boxplot
```python
sns.boxplot(data=df, x="cat_column", y="column")
```

### violinplot
```python
sns.violinplot(data=df, x="cat_column", y="column")
```

### scatterplot
```python
sns.scatterplot(data=df, x="column1", y="column2", hue="cat_column")
```

### regplot
```python
sns.regplot(data=df, x="column1", y="column2")
```

### lmplot
```python
sns.lmplot(data=df, x="column1", y="column2", hue="dataset")
sns.lmplot(data=df, x="column1", y="column2", hue="dataset", col="dataset", col_wrap=2, ci=None)
```

### kdeplot
```python
sns.kdeplot(data=df, x="column")
sns.kdeplot(data=df, x="column", cut=15)
```

### histplot
```python
sns.histplot(data=df, x="column", bins=10)  # bins : 구간
```
