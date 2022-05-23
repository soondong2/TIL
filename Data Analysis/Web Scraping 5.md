# Today I Learned - 2022/05/23 Mod

# ETF
ETF(상장지수펀드)는 기초지수의 성과를 추적하는 것이 목표인 인덱스펀드로, 거래소에 상장되어 있어서 개별주식과 마찬가지로 기존의 주식계좌를 통해 거래를 할 수 있다.

<br>

## 크롬 브라우저의 네트워크 정보를 통한 데이터 수집

- json 데이터 수집과 파일저장 방법
```python
import pandas as pd
import numpy as np
import requests
from bs4 import BeautifulSoup as bs
```

```python
url = "https://finance.naver.com/api/sise/etfItemList.nhn?etfType=0&targetColumn=market_sum&sortOrder=desc"
print(url)

# pd.read_html(url) 이걸로는 불러올 수 없음
```

# JSON

`JSON` (제이슨, JavaScript Object Notation)은 `속성-값`  쌍( attribute–value pairs and array data types (or any other serializable value)) 또는 "키-값 쌍"으로 이루어진 데이터 오브젝트를 전달하기 위해 인간이 읽을 수 있는 텍스트를 사용하는 개방형 표준 포맷이다.

<br>

## requests를 통한 HTTP 요청

```python
response = requests.get(url)
response  # 200
```

## JSON 타입으로 데이터 받기

```python
etf_json = response.json()
```

## JSON 에서 원하는 데이터 찾기

```python
etfItemList = etf_json["result"]["etfItemList"]
etfItemList[0]
```

## JSON 데이터를 pandas 의 데이터프레임으로 만들기

```python
df = pd.DataFrame(etfItemList)
```

## 파일 저장

```python
from datetime import datetime
today = datetime.today().strftime('%Y-%m-%d')  # '2022-05-23'
file_name = f"eft_{today}_raw.csv"

df.to_csv(file_name, index=False)
pd.read_csv(file_name, dtype={"itemcode": "object"})
```
