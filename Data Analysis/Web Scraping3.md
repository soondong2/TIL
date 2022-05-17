# Today I Learned - 2022/05/17 Tue

# Naver finance daily Web scraping
`table`  태그가 들어감에도 불구하고 `read_html` 을 사용할 수 없을 때 사용하는 방법이다.

## 라이브러리
```python
import pandas as pd
import numpy as np
import requests
```

## 수집할 URL 정하기
```
item_code = "323410"
item_name = "카카오뱅크

item_code = "005930"
item_name = "삼성전자"
```

```python
# 종목번호와 상장사 이름을 item_code와 item_name으로 설정

item_code = "005930"
item_name = "삼성전자"

url = f"https://finance.naver.com/item/sise_day.naver?code={item_code}&page=1"
print(url)
```

`[https://finance.naver.com/item/sise_day.naver?code=005930&page=1](https://finance.naver.com/item/sise_day.naver?code=005930&page=1)`

## Pandas read_html로 불러오기
table 태그로 되어있음에도 불구하고 데이터를 불러올 수 없는 오류가 발생한다.

```python
table = pd.read_html(url, encoding="cp949")

print(len(table))
table[0]
```

### 📝 euc-kr과 cp949의 차이점

|  | euc-kr | cp949 |
| --- | --- | --- |
| 차이점 | 2350자 | 11172자 |

## requests를 통한 HTTP 요청
`Request Method` 에 `GET` 이라고 되어 있으므로 `requests.get` 을 이용하여 가져온다.

로봇인지 아닌지를 판별할 수 있도록 USER의 Agent 정보를 Header에 입력해주어야 한다.

```python
headers = {'user-agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.67 Safari/537.36'}

requests.get(url)  # <Response [200]> 라고 나타나면 정상적으로 작동한 것이다.

response = requests.get(url, headers=headers)
response.status_code  # 200으로 나타나면 정상적으로 작동한 것이다.

response.text
```

```python
print(headers, type(headers), headers["user-agent"])
# {'user-agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.67 Safari/537.36'} <class 'dict'> Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.67 Safari/537.36
```

### 📝 HTTP 상태 코드

| 코드 | 상태 | 설명 |
| --- | --- | --- |
| 100 | 정보 | 요청을 받았으며 프로세스를 계속한다. |
| 200 | 성공 | 요청을 성공적으로 받았으며 수용했다. |
| 300 | 리다이렉션 | 요청 완료를 위해 추가 작업 조치가 필요하다. |
| 400 | 클라이언트 오류 | 오류 요청의 문법이 잘못되었거나 요청을 처리할 수 없다. |
| 500 | 서버 오류 | 서버가 명백히 유효한 요청에 대해 실패했다. |

## BeautifulSoup 을 통한 table 태그 찾기

`lxml` 이나 `html` 을 보기 좋게 출력하기 위해 사용하는 모듈이다.

`response.text` 에 비해 훨씬 깔끔하고 보기 좋게 출력된다.

<참고 문서>

[https://www.crummy.com/software/BeautifulSoup/bs4/doc/](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)

```python
from bs4 import BeautifulSoup as bs

soup = bs(response.text, "lxml")
soup
```

```python
soup.title  # <title>네이버 금융</title>
soup.find_all('a')
soup.find_all('table')
soup.table  # table 태그 찾기
```

- 주의 ❗ `list` 로는 읽어들일 수 없기 때문에 `str` 형식으로 바꿔서 사용한다.

```python
tables = soup.select("table")  # find_all과 동일한 결과가 나타난다.

table = pd.read_html(str(tables), encoding="cp949")

print(len(table))
table[0]
```

### requests → BeautifulSoup → pd.read_html 과정 이유❓

<aside>
💡 정상적인 접근인지를 확인하기 위해서이다.

</aside>

### 📝 파서의 사용법 및 장단점

| 파서 | 사용범 | 장점 및 단점 |
| --- | --- | --- |
| html.parser | BeautifulSoup(markup, "html.parser") | lxml 보다는 빠르지 않지만 html5lib보다는 빠르다. |
| lxml | BeautifulSoup(markup, "lxml") | 매우 빠르지만 허술하다 |
| lxml-xml | BeautifulSoup(markup, "lxml-xml") | 매우 빠르다 |
| html5lib | BeautifulSoup(markup, "html5lib") | 매우 관대하다 |

```python
temp = table[0].dropna(how="all", axis=0)  # 결측치 제거
temp
```

## 페이지별 데이터 수집 함수 만들기

```python
def get_day_list(item_code, page_no):
    
    url = f"https://finance.naver.com/item/sise_day.naver?code={item_code}&page={page_no}"
    headers = {'user-agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.67 Safari/537.36'}

    response = requests.get(url, headers=headers)
    soup = bs(response.text, "lxml")

    tables = soup.select("table")
    table = pd.read_html(str(tables), encoding="cp949")

    df = table[0].dropna(how="all", axis=0)
    
    return df
```

```python
item_code = "005930"
item_name = "삼성전자"
page_no = 1

get_day_list(item_code, page_no)
```

## 반복문을 통한 전체 일자 데이터 수집하기

### 1. for문

```python
import time
from tqdm import trange

page_no = 1
item_list = []

for page in trange(page_no, 11):
    page = get_day_list(item_code, page)
    item_list.append(page)
    time.sleep(0.5)

df = pd.concat(item_list, axis=0)
df.head()
```

### 2. while

```python
page_no = 1
item_list = []

last_page = soup.find_all('a')[-1]["href"].split("=")[-1]  # 14

while True:
    page = get_day_list(item_code, page_no)
    item_list.append(page)
    time.sleep(0.5)
    
    page_no += 1
    
    if page_no == int(last_page) + 1:
        break
```

### 3. while

```python
page_no = 1
item_list = []

item_code = "377300"
item_name = "카카오페이"

prev = ""

while True:
    one_page = get_day_list(item_code, page_no)
    curr = one_page.iloc[-1, 0]  # 마지막 날짜
    
    # 마지막 날짜를 비교
    if curr == prev:
        break
        
    item_list.append(one_page)
    page_no += 1
    
    prev = curr  # 현재 날짜를 이전 날짜 변수에 담아서 다음 번에 비교한다.
```

- 수집한 데이터 하나의 데이터프레임으로 합치기
- 데이터프레임에 종목코드와 종목명 추가
- 컬럼 순서 변경
- 중복 데이터 제거
- 최근 날짜 구해서 파일명 만들기

```python
df = pd.concat(item_list, axis=0)

df["종목코드"] = item_code
df["종목명"] = item_name

cols = ['종목코드', '종목명', '날짜', '종가', '전일비', '시가', '고가', '저가', '거래량']
df = df[cols]

df = df.drop_duplicates()
df = df.drop_duplicates("날짜")  # 날짜가 같은 중복 값을 제거

date = max(df["날짜"])

file_name = f"{item_name}_{item_code}_{date}"  # '카카오페이_377300_2022.05.17'

df.to_csv(file_name, index=False)
pd.read_csv(file_name)
```
