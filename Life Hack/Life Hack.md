# 카테고리에 정리하기 애매한 꿀팁 모음집1
## 1. \
- 아래와 같이 긴 코드를 작성하는 경우 복잡하고 보기 힘들어진다.
```python
train.iloc[:, :-1].describe().T.sort_values(by="std", ascending=False).style.background_gradient(cmap="GnBu")
```
<br>

- `\`를 사용하면 긴 코드를 보기 좋게 정리하여 작성할 수 있다.
```python
train.iloc[:, :-1].describe().T.sort_values(by="std", ascending=False)\
    .style.background_gradient(cmap="GnBu")\
```
<br>

## 2. background_gradient()
- `.style.background_gradient`를 통해 데이터프레임에 크기에 따라서 색상을 입혀 강조할 수 있다.
```python
.style.background_gradient(cmap="GnBu")
```
<br>

## 3. .bar()
- `.bar(subset=["column"]m color="색상")`을 입력해주면 해당 컬럼을 해당 색상으로 강조할 수 있다.
```python
.bar(subset=["max"], color="#BB0000")
```
<br>
