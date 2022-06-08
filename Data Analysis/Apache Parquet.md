# Today I Learned - 2022/06/08 Wed

## Apache Parquet
- 효율적인 데이터 저장 및 검색을 위해 설계된 오픈 소스, 열 지향 데이터 파일 형식
- 복잡한 데이터를 대량으로 처리하기 위해 향상된 성능과 함께 효율적인 데이터 압축 및 인코딩 체계를 제공
- Parquet은 Java, C++, Python 등을 포함한 여러 언어를 지원
- Twitter 와 Cloudera 의 협업으로 만들어졌습니다.
- Hadoop 창시자인 더그커팅의 trevni 열 저장 형식을 개선하기 위해 설계 되었습니다.
- 열의 값은 물리적으로 인접한 메모리 위치에 저장됩니다.
- 열 단위 압축은 효율적이고 저장 공간을 절약합니다.
- 열 값이 동일한 데이터 타입이기 때문에 압축에 유리합니다.
- 특정 열 값을 가져오는 쿼리는 전체 행 데이터를 읽을 필요가 없으므로 성능이 향상됩니다.
- 각 열에 다른 인코딩 기술을 적용할 수 있습니다.
- 열 스토리지, 필요한 데이터만 읽기
- 효율적인 바이너리 패킹
- 압축 알고리즘 및 인코딩 선택
- 데이터를 파일로 분할하여 병렬 처리 가능
- 논리 유형의 범위
- 메타데이터에 저장된 통계를 통해 불필요한 청크를 건너뛸 수 있습니다.
- 디렉토리 구조를 사용한 데이터 분할

<br>

## 라이브러리
```python
import pandas as pd
import numpy as np
```

<br>

## to_parquet 동작확인
- fastparquet와 pyarrow를 설치했음에도 로컬 PC에서 아래 코드가 동작하지 않는다면 colab 권장
- fastparquet와 pyarrow는 관련된 라이브러리 버전의존성 이슈가 있어서 버전이 맞지 않으면 동작하지 않을 수 있다.

```python
df = pd.DataFrame(data={'col1': [1, 2], 'col2': [3, 4]})
df.to_parquet('df.parquet.gzip', compression='gzip')
```

<br>

## 데이터 프레임 만들기
```python
df = pd.read_csv("C:/Users/user/Desktop/data/Lion/nhis_drug_sample_2020_3.csv")
```
<br>

- 파일 저장
- `parquet` 형식과 `csv` 형식으로 저장
```python
file_path_parquet = 'df.parquet.gzip'
file_path_csv  = 'df.csv'

df.to_parquet('df.parquet.gzip', compression='gzip')
df.to_csv(file_path_csv, index=False)
```

<br>

- 용량 사이즈
```python
import os

format(os.stat(file_path_parquet).st_size, ",")  # 2,835,603
format(os.stat(file_path_csv).st_size, ",")  # 26,064,481
```

<br>

## 파일 크기
- 파일 크기 반환하는 함수
- 소수점 둘 째자리까지 `num:.2f` 또는 `round(, 2)` 를 사용한다.

```python
num = 26064481

for fs in ['bytes', 'KB', 'MB', 'GB', 'TB']:
    if num < 1024:
        print(f"{num:.2f} {fs}")
        break
        
    num /= 1024
```
<br>

- 파일 사이즈를 bytes로 표기하는 함수
```python
def convert_bytes(num):
    """
    1024 보다 크면 숫자를 나누고 아니면 숫자와 단위를 표시하도록
    for문을 돌면서 값을 1024로 나누고 
    값이 1024 보다 작다면 단위와 함께 num 을 반환
    """
    for fs in ['bytes', 'KB', 'MB', 'GB', 'TB']:
        if num < 1024:
            return f"{num:.2f} {fs}"
        
        num /= 1024
```

```python
def file_size(file_path):
    """
    파일이 있다면 convert_bytes 함수를 통해 크기를 구함
    """
    if os.path.isfile(file_path):
        file_info = os.stat(file_path)
        return convert_bytes(file_info.st_size)

file_size(file_path_parquet), file_size(file_path_csv)
# ('2.70 MB', '24.86 MB')
```

⇒  parquet을 사용했을 때와 아닐 때에 파일 크기가 약 12배 차이가 난다.

<br>

- 파일 저장하고 사이즈 비교하는 함수

```python
def compare_csv_parquet(df):
    """
    데이터프레임을 csv 와 parquet형식으로 저장하하고 각 파일 사이즈를 dict 형태로 반환
    """
    file_path_parquet = 'df.parquet.gzip'
    file_path_csv  = 'df.csv'
    
    df.to_parquet(file_path_parquet, compression='gzip')
    df.to_csv(file_path_csv, index=False)
    
    parquet = file_size(file_path_parquet)
    csv = file_size(file_path_csv)
    
    return {"parquet":parquet, "csv":csv}
```

```python
compare_csv_parquet(df)  # {'parquet': '2.70 MB', 'csv': '24.86 MB'}
```
<br>

- 다른 데이터 사이즈 비교

```python
df = pd.read_csv("C:/Users/user/Desktop/data/Lion/seoul-covid19-2021-12-18.csv")
compare_csv_parquet(df)  # {'parquet': '1.46 MB', 'csv': '13.25 MB'}
```

⇒ parquet을 사용했을 때와 아닐 때에 파일 크기가 약 13배 차이가 난다.

<br>

## Data Load 속도 비교

- parquet

```python
%time pd.read_parquet(file_path_parquet)

# CPU times: total: 375 ms
# Wall time: 295 ms
```

- csv

```python
%time pd.read_csv(file_path_csv)

# CPU times: total: 594 ms
# Wall time: 604 ms
```

⇒ 메모리 사용량은 같지만, parquet의 처리 속도가 훨씬 빠르다.

<br>

## 단점
- 압축을 많이 할 경우 텍스트, 엑셀 프로그램에서 바로 열 수 없다.
- 별도의 프로그램 사용이 필요하다.

<br>

## PySpark Koalas

- `Spark`란 ❓
- 대용량 데이터를 처리하기 위한 분산 처리 플랫폼 (pandas와 같은 데이터 분석 도구)
- `pyspark`는 파이썬환경에서 쓸 수 있게해주는 인터페이스

```python
import pyspark.pandas as pd
```
