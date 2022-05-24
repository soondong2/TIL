# Today I Learned - 2022/05/24 The

# EDA

## 시각화를 위한 폰트 설정
```python
import platform

def get_font_family():
    system_name = platform.system()
    # colab 사용자는 system_name이 'Linux'로 확인

    if system_name == "Darwin" :
        font_family = "AppleGothic"
    elif system_name == "Windows":
        font_family = "Malgun Gothic"
    else:
        !apt-get install fonts-nanum -qq  > /dev/null
        !fc-cache -fv

        import matplotlib as mpl
        mpl.font_manager._rebuild()
        findfont = mpl.font_manager.fontManager.findfont
        mpl.font_manager.findfont = findfont
        mpl.backends.backend_agg.findfont = findfont
        
        font_family = "NanumBarunGothic"
    return font_family

# 그래프에 retina display 적용
%config InlineBackend.figure_format = 'retina'
```
<br>

- `print(plt.style.available)` 를 통해 matplotlib의 그래프 스타일 목록들을 볼 수 있다.
```python
import matplotlib.pyplot as plt
plt.style.use("ggplot")

# 폰트설정
plt.rc("font", family=get_font_family())

# 마이너스폰트 설정
plt.rc("axes", unicode_minus=False)
```
<br>

## 서브플롯
- `subplots=True` : 서브플롯을 그려준다.
- `_` = 그래프 : 그래프를 깔끔하게 볼 수 있게 해준다.
- `plt.show()` : 그래프를 깔끔하게 볼 수 있게 해준다.
- `secondary_y="column2"` : column1은 왼쪽, column2는 오른쪽으로 설정되며 스케일링 진행 후 그래프를 그린 것과 같은 결과가 나타난다.
```python
df.plot(subplots=True)

df[["column1", "column2"]].plot(secondary_y="column2")
```
