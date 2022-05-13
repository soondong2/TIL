# Today I Learned - 2022/05/09 Mon

## 📌 함수
```python
def 함수명(매개변수):
  실행할 소스 코드
  return 반환할 값
```

- `global` : 함수 밖에 선언된 변수를 참조

### 📌 람다 표현식
```python
print((lambda a, b: a + b)(3, 7))
```

```python
array = [('A', 50), ('B', 32), ('C', 74]

def my_key(x):
  return x[1]   # value를 기준으로 정렬
  
print(sorted(array, key=my_key)
```

```python
print(sorted(array, key=lambda x: x[0]  # key를 기준으로 정렬
```

## 📌 기타
### random
```python
import random

random.choice()
random.sample(랜덤 범위, 개수)
```

```python
print(random.sample(range(1, 45), 6)) # [22, 39, 19, 27, 38, 9]
```
