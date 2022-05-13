# Today I Learned - 2022/05/10 Tue ~ 2022/05/11 Wed
---
## 📌 Seaborn
- matplotlib을 추상화 해놓은 시각화 도구이다.

- seaborn의 그래프 스타일은 `darkgrid` , `whitegrid` , `dark` , `white` , `ticks` 5가지가 존재한다.
- 아래 코드를 통해 matplotlib의 그래프 종류가 어떤 것들이 있는지 알아볼 수 있다.

### countplot
- 범주형 변수의 분포를 알아볼 때 사용한다.
```python
sns.countplot(data=df, x="cat_column")  # 세로 축
sns.countplot(data=df, y="cat_column")  # 가로 축
```

### barplot
- barplot은 default로 평균으로 그래프가 그려진다.
- `ci`를 통해 표준편차로 변경하여 그릴 수 있다.
```python
sns.barplot(data=df, x='cat_column', y="column")
sns.barplot(data=df, x='cat_column', y="column", ci="sd")
```

### boxplot
- `상자그림`을 통해 이상치, 중위수(Q3, 제 3사분위수), 제 1사분위수(Q1), 제 2사분위수(Q3), 최대값, 최소값을 알 수 있다.
```python
sns.boxplot(data=df, x="cat_column", y="column")
```

### violinplot
```python
sns.violinplot(data=df, x="cat_column", y="column")
```
![image](https://user-images.githubusercontent.com/100760303/168299863-8cc28d66-766b-4677-953e-f1e6916e1f05.png)

### scatterplot
- `산점도`라고 한다.
- 수치형 변수의 경우에 사용할 수 있다.
```python
sns.scatterplot(data=df, x="column1", y="column2", hue="cat_column")
```

### regplot
```python
sns.regplot(data=df, x="column1", y="column2")
```
![image](https://user-images.githubusercontent.com/100760303/168299300-fff8980e-33e1-43e1-bf50-3955803c5dc3.png)

### lmplot
```python
sns.lmplot(data=df, x="column1", y="column2", hue="dataset")
```
![image](https://user-images.githubusercontent.com/100760303/168299575-cb6fd382-a93f-4868-bd96-de02e4930697.png)

```python
sns.lmplot(data=df, x="column1", y="column2", hue="dataset", col="dataset", col_wrap=2, ci=None)
```
![image](https://user-images.githubusercontent.com/100760303/168299664-327b4291-c0c0-4205-b65d-b4bc27e885a8.png)

### kdeplot
```python
sns.kdeplot(data=df, x="column")
sns.kdeplot(data=df, x="column", cut=15)
```

### histplot
```python
sns.histplot(data=df, x="column", bins=10)  # bins : 구간
```
### Jointplot
- kind = ["kde", "scatter", "hist", "hex"]
```python
sns.jointplot(data=df, x="column", y="column", kind="scatter")
```

### pairplot
- 모든 쌍의 그래프를 그려준다.
- 시간이 오래 걸린다는 단점이 있다.
- 대각선으로는 히스토그램, 비대각선으로는 산점도를 그려준다.
```python
sns.pairplot(data=df, hue="cat_column")
```

### lineplot
```python
sns.lineplot(data=df, y="column", x="column")
```

### 결측치 시각화
```python
sns.heatmap(df.isnull())
```
![image](https://user-images.githubusercontent.com/100760303/168302016-ce6b6850-0185-4233-92bb-c7e42e9aeee9.png)

### heatmap
```python
mask = np.triu(np.ones_like(corr))
mask
```

```
[[1., 1., 1., 1., 1., 1., 1.],
 [0., 1., 1., 1., 1., 1., 1.],
 [0., 0., 1., 1., 1., 1., 1.],
 [0., 0., 0., 1., 1., 1., 1.],
 [0., 0., 0., 0., 1., 1., 1.],
 [0., 0., 0., 0., 0., 1., 1.],
 [0., 0., 0., 0., 0., 0., 1.]]
```

```python
sns.heatmap(corr, annot=True, cmap="coolwarm", mask=mask, vmin=-1, vmax=1)
```

- `annot=True` : 상관계수를 그래프에 나타낸다.
- `vmin=-1`, `vmax=1` : 가장 작은 값과 가장 큰 값의 색상을 강조한다.
- `cmap` : 그래프 색상을 나타낸다.

```python
print(plt.colormaps()) # cmap으로 가능한 색상들을 보여준다.
```
