# Today I Learned - 2022/05/16 Mon

# Web Scraping
## 라이브러리

- `finance-datareader` : 한국증권정보 및 금융 정보를 받아올 수 있다.

```python
!pip install -U finance-datareader
!pip install requests
!pip install BeautifulSoup4
!pip install tqdm
```

- `.__version__` : 라이브러리의 버전을 확인할 때 사용한다.**
- `%pwd` : working directory를 확인할 때 사용한다.
- `Shift + tab` : 도움말

## fdr.DataReader

```python
import pandas as pd
import FinanceDataReader as fdr
```

```
KRX : KRX 종목 전체
KOSPI : KOSPI 종목
KOSDAQ : KOSDAQ 종목
KONEX : KONEX 종목
NASDAQ : 나스닥 종목
NYSE : 뉴욕증권거래소 종목
SP500 : S&P500 종목
```

fdr.DataReader의 도움말을 확인해보면 다음과 같다.
```python
fdr.DataReader(
    symbol,
    start=None,
    end=None,
    exchange=None,
    data_source=None,
)
```

- `symbol` : 035720은 삼성전자를 나타낸다.
- 2020년도의 데이터만 보여준다.

```python
df = fdr.StockListing("krx")  # 한국거래소 상장종목 전체 가져오기

fdr.DataReader("035720", "2020")  # 삼성전자
```

## Pandas로 Scraping 하기
![image](https://user-images.githubusercontent.com/100760303/168578803-1c526e3c-4b5e-442c-8b4a-5fc1c836680b.png)

- `page_no` : 페이지 번호
- `item_code` : 보고자 하는 곳에 해당하는 코드

```python
item_code = "005930"
item_name = "삼성전자"
page_no = 1

url = f"https://finance.naver.com/item/news_news.nhn?code={item_code}&page={page_no}&sm=title_entity_id.basic&clusterId="
print(url)
```

## ****read_html****

네이버 금융의 주가 기사를 read_html로 수집해서 table 이라는 변수에 담는다.

- 한글이 깨질 경우 : `encoding="utf-8"` 또는 `encoding="cp949”`

```python
table = pd.read_html(url, encoding="cp949")
table
```

>table을 살펴보니 len(table) = 5이며, 제일 마지막 페이지인 table[4]에 기사 내용이 전혀 담겨 있지 않는다.  
이는 페이지 번호를 나타내는 것이기 때문에 분석에 필요없으므로 제거해준다.

```python
cols = table[0].columns
temp_list = []

for news in table[:-1]:  # 마지막 페이지 제거
    news.columns = cols
    temp_list.append(news)

df_temp = pd.concat(temp_list)
df_temp = df_temp[~df_temp["제목"].str.contains("연관기사")]  # ~는 not을 의미
```

>`new.columns = cols` 를 해주는 이유는 table[0]은 제목, 정보제공, 날짜가 컬럼명으로 지정되어 있지만 table[1] 부터는 컬럼명이 0, 1, 2로 지정되어 있기 때문에 `pd.concat` 으로 데이터를 합쳐줄 경우 컬럼명이 다르므로 `NaN` 값이 생성된다.따라서 컬럼명을 동일하게 제목, 정보제공, 날짜로 통일해준 후 합쳐준다.  이후 연관기사가 들어간 내용들을 제거해준다.
