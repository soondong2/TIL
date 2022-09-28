# Today I Learned - 2022/09/28 Wed

# Matplotlib
- 참고 사이트 : https://wikidocs.net/book/5011
- Matplotlib의 기본적인 사용 방법은 위 사이트에서 참고한다.
- 아래는 그 외 몰랐던 걸 공부한 부분들을 정리해놓은 것이다.
<br>

## matplotlib.axes.Axes.tick_params
- 공식문서 : https://matplotlib.org/stable/api/_as_gen/matplotlib.axes.Axes.tick_params.html
- tick_params함수로 눈금의 스타일 설정할 수 있다.
<br>

- `axis` : 축 지정 ["x", "y", "both"] 중 선택
- `direction` : 눈금이 안/밖으로 표시 ["in", "out", "inout"] 중 선택
- `length` : 눈금의 길이, pad : 눈금과 레이블의 길이
- `labelsize` : 레이블 크기
- `labelcolor` : 레이블 색상
- `top/bottom/left/right` : True/False로 지정하면 눈금이 표시될 위치 선택
- `width` : 눈금의 너비
- `color` : 눈금의 색상
<br>

>example
```python
ax.tick_params(direction='out', length=6, width=2, colors='r',
               grid_color='r', grid_alpha=0.5)
```
