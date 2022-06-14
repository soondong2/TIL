# Today I Learned - 2022/06/13 Mon

## 리눅스 명령어

- `s` : 현재 디렉토리 폴더 내부 확인 (윈도우 dir)
- `ls -l` : 현재 디렉토리에 위치한 파일 상세정보 확인
- `ls -a` : 현재 directory에 위치한 숨겨진 파일정보 포함 확인
- `cd` : Change 디렉토리, 현재 디렉토리 위치에 존재하거나 상위 다른 디렉토리로 이동
- `cd ~` : root 디렉토리 이동
- `cd ..` : 상위 디렉토리 이동
- `mkdir dirName` : 현재 디렉토리 위치에서 새로운 디렉토리를 생성
- `mv` 디렉토리 혹은 파일 `이동경로` : 현재 디렉토리 내 디렉토리 또는 파일 이동
- `mv` 디렉토리 혹은 파일 `newName` : 현재 디렉토리 내 디렉토리 또는 파일 이름 변경
- `cp` 현재파일명 복사할파일명 : 현재 디렉토리 내 파일 복사
- `cp -R dir/` : 현재 디렉토리 내 디렉토리 복사
- `rm fileName` : 현재 디렉토리 내 파일 삭제
- `rm -rf` : 현재 디렉토리 내 디렉토리 삭제

<br>

## requirements.text
- 반드시 필요하다

<br>

## 가상환경
```
conda activate base  : 가상환경 활성화
conda deactibate  : 가상환경 비활성화
Ctrl + C : 서버 종료
```

<br>

```python
pip install streamlit  # streamlit 설치

import streamlit as st
import pandas as pd

st.write(
"""
# My first app
Hello World!
"""
)

df = pd.read_csv("data.csv")
st.line_chart(df)
```

<br>

### Github 배포
- Github 레포지토리 생성
- requirements.txt
```python
    pandas
    numpy
    streamlit
    finance-datareader
    plotly
    seaborn
    matplotlib
    koreanize_matplotlib  # streamlit 한글 폰트 설정
```
→ 필요한 라이브러리들을 자동으로 설치하고 설정해준다.

<br>

- streamlit에 나타낼 코드 파일 업로드
- streamlit 로그인 → GIthub 연동 → 업로드 → 풍선이 날아가면 성공!

<br>

## page 만들기
- Github에 pages 폴더 생성 후 mpg.py 파일 생성 후 코드 입력 후 업로드
- streamlit에서 Reboot App 클릭 또는 새로고침
- Github에 pages에 .py 파일 추가 후 새로고침
