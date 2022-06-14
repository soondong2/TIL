# Today I Learned - 2022/06/08 Wed

## 라이브러리

```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
```
<br>

## Data Load

```python
file_name = "C:/Users/user/Desktop/data/Lion/bike_station.csv"
df = pd.read_csv(file_name)
```
<br>

## folium

```python
import folium
folium.Map()
```

```python
# 지도의 중심을 잡기 위한 위도, 경도
lat = df["위도"].mean()
long = df["경도"].mean()
```

```python
folium.Map(location=[lat, long], zoom_start=12)
```

```python
m = folium.Map(location=[lat, long], zoom_start=12)

for bst in df.index:
    row = df.loc[bst]
        
    folium.Circle(
        radius=int(row["자전거수"]),
        location=[row["위도"], row["경도"]],
        tooltip=str(row["자전거수"]) + row["대여소명"] + "_ <br/>" + row["상세주소"],
        color = {"QR" : "red", "LCD" : "green"}[row["운영방식"]],
        fill=False
    ).add_to(m)
m
```
