# Today I Learned - 2022/05/18 Wed

# 서울특별시 다산콜센터(☎120)의 주요 민원

[https://opengov.seoul.go.kr/civilappeal/list](https://opengov.seoul.go.kr/civilappeal/list)<br>
[https://opengov.seoul.go.kr/civilappeal/25670204](https://opengov.seoul.go.kr/civilappeal/25670204)

위 주소는 민원 목록이 담긴 페이지가 보이는 화면이고, 아래 주소는 민원 내용이 담겨있다.<br>
두 주소의 마지막 부분이 `list` 와 `25670204` 으로 다르게 나타난다. 이를 어떻게 해결하면 좋을까❓

```python
import pandas as pd
import numpy as np
import requests
from bs4 import BeautifulSoup as bs
```

```python
url = "https://opengov.seoul.go.kr/civilappeal/list?items_per_page=50&page=2"
```

- **Content-Type :**  text/html; charset = `UTF-8` 이라고 되어있음을 확인한다.

```python
table = pd.read_html(url, encoding="utf-8")
```
<br>

## 상세정보를 위한 링크정보 수집

- `GET` : 필요한 데이터를 Query String 에 담아 전송
- `POST` : 전송할 데이터를 HTTP 메시지의 Body의 Form Data에 담아 전송
- `GET` 과 `POST` 여부는 브라우저의 `Network` 탭의 `Headers` > `Request Method` 를 통해 확인

```python
response = requests.get(url, 'lxml')
response.status_code  # 200으로 나타나면 정삭적으로 작동함을 의미한다.
```
<br>

## BeautifulSoup 을 통해 html 페이지 불러오기
```python
html = bs(response.text, 'lxml')
```
<br>

## 상세 정보 수집을 위한 링크 정보 찾기
`Inspect` 로 확인 해보니 table > a 태그 안에 들어있다.<br>
마우스 우클릭 > `Copy` > `Copy Selector`  를 하면 아래와 같은 경로를 알아낼 수 있다.<br>
content > div > div.view-content > div > table > tbody > tr:nth-child(1) > td.data-title.aLeft > a

```python
a_list = html.select("#content > div > div.view-content > div > table > tbody > tr > td > a")
a_list
```
<br>

`<a href="/civilappeal/25670204">다자녀가정 실내 바닥매트 지원</a>` 에서 `25670204` 만 가져온다.<br>
아래의 두 코드는 같은 결과를 나타내는 코드이다.

###  1. 리스크 컴프리헨션
```python
num = [a_list[i]["href"].split("/")[-1] for i in range(len(a_list))]
df_table["내용번호"] = num
```

### 2. for문
```python
for i in range(len(a_list)):
    df_table.loc[i, "내용번호"] = a_list[i]["href"].split("/")[-1]
```
<br>

## 특정 페이지를 수집하는 함수
위 과정들을 하나의 함수로 만든다.

```python
def get_one_page(page_no):

    url = f"https://opengov.seoul.go.kr/civilappeal/list?items_per_page=50&page={page_no}"
    headers = {'user-agent' : 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.67 Safari/537.36'}
    response = requests.get(url, headers=headers)
    
    df_table = pd.read_html(response.text)[0]
    
    if len(df_table.values) == 0:
            return f"{page_no} 페이지를 찾을 수 없습니다."

    try:
        html = bs(response.text, 'lxml')
        
        a_list = html.select("#content > div > div.view-content > div > table > tbody > tr > td > a")

        num = [a["href"].split("/")[-1] for a in a_list]
        df_table["내용번호"] = num
        
    except:
        return f"{page_no} 페이지를 찾을 수 없습니다."
    
    return df_table
```

```python
get_one_page(1)
get_one_page(50)
get_one_page(51)
```
<br>

## 반복문을 통한 여러 페이지 수집

```python
import time

page_no = 1
table_list = []

while True:
    df = get_one_page(page_no)
    
    if type(df) == str:
        break

    else:
        table_list.append(df)
        page_no += 1
    
    time.sleep(0.05)
```
<br>

## 데이터 병합 및 파일 저장

```python
df = pd.concat(table_list)

file_name = "seoul-120-list.csv"
df.to_csv(file_name, index=False)
pd.read_csv(file_name)
```
<br>

## 📝 HTML
|  | id | class |
| :---: | :---: | :---: |
| 정의 | 속성은 요소에 대한 문서 전체의 고유 식별자를 제공한다. | 속성은 유사한 요소를 분류하는 방법을 제공한다. |
| 접근 방법 | ID는 하나의 요소에만 적용할 수 있다. 앞에 # 이  붙는다. | 앞에 . 이 붙는다. |

| 태그 | 내용 |
| :---: | :---: |
| table | 표만들기 |
| tr | 행에 넣는다) |
| td | 열에 넣는다) |
| td colspan=숫자 | 그 셀부터 숫자만큼의 오른쪽 셀을 병합한다 |
| td rowspan=숫자 | 그셀부터 숫자만큼의 아래쪽 셀을 병합한다 |
| br | 줄바꾸기 |
| p | 단락바꾸기(한줄 떨어짐) |
| hr | 가로줄 |
