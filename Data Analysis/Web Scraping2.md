# Today I Learned - 2022/05/17 Tue

# Naver finance news Web scraping
Pandas 의 `read_html` 을 통한 데이터 수집하는 방법에 대해 알아본다.

## URL 받아오는 함수

```python
def get_url(item_code, page_no):
    url = f"https://finance.naver.com/item/news_news.nhn?code={item_code}&page={page_no}&sm=title_entity_id.basic&clusterId="
    return url
```

## 뉴스 한 페이지를 수집하는 함수

```python
1) URL 을 받아옴
2) read_html 로 테이블 정보를 받아옴
3) 데이터프레임 컬럼명을 ["제목", "정보제공", "날짜"]로 변경
4) temp_list 에 데이터프레임을 추가
5) concat 으로 리스트 병합하여 하나의 데이터프레임으로 만들기
6) 결측치 제거
7) 연관기사 제거
8) 데이터프레임 반환
```

```python
def get_one_page_news(item_code, page_no):

    url = get_url(item_code, page_no)
    table = pd.read_html(url, encoding="cp949")
    
    temp_list = []
    cols = table[0].columns
    
    for news in table[:-1]:
        news.columns = cols
        temp_list.append(news)
    
    df_temp = pd.concat(temp_list)
    df_temp = df_temp.dropna(how="all", axis=0).dropna(how="all", axis=1)
    df = df_temp[~df_temp["제목"].str.contains("연관기사")]
    
    return df
```

```python
page_no = 1
item_code = "005930"  # 삼성 전자
item_code = "035720"  # 카카오

temp = get_one_page_news(item_code, page_no).reset_index(drop=True)
temp
```

## 반복문을 사용해 10페이지까지 수집

- 위에서 만든 함수를 활용한다.
- `time.sleep()`  을 통해 데이터를 쉬었다 가져온다.

```python
import time
from tqdm import trange

item_code = "005930"  # 삼성전자
item_code = "035720"  # 카카오

page_no = 0
news_list = []

for page_no in trange(1, 11):
    page = get_one_page_news(item_code, page_no)
    time.sleep(1)
    news_list.append(page)
    
print(news_list)
```

## 데이터프레임으로 만들고 파일 저장

```python
df_news = pd.concat(news_list, axis=0).reset_index(drop=True)
```

```python
item_code = "035720"
item_name = "카카오"

file_name = f"news_{item_code}_{item_name}.csv"  # 'news_035720_카카오.csv'

df_news.to_csv(file_name, index=False)
pd.read_csv(file_name)
```

## tqdm 모듈

<aside>
💡 반복문과 같은 수행시간이 긴 연산을 하다보면 내부에서 잘 처리되고 있는지 확인하기 어렵다. print함수를 이용하여 중간 중간 iteration을 출력해 볼 수 있으나 화면이 지저분해진다는 단점이 있다.  이런 경우 Progress Bar를 지원하는 `tqdm` 모듈을 사용한다.

</aside>

### trange()

```python
for i in trange(10):
	print(i)
```

### tqdm(range())

```python
for i in tqdm(range(10)):
	print(i)
```
