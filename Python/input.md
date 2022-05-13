# Today I Learned - 2022/05/09 Mon

## 입출력
- `map()` : 리스트의 모든 원소에 각각 특정한 함수 적용
```python
a, b, c = map(int, input().split())
```

- 입력을 최대한 빠르게 받아야 하는 경우 사용
```python
import sys
data = sys.stdin.readline().rstrip()
```

- 기본적으로 출력 이후 줄 바꿈을 수행하므로 원치 않을 경우 `end` 사용
```python
print(, end=" ")
```

- `f-string`
```python
a = "뚱"
print(f"아뇨, {a}인데요?")
```

```python
a = "뚱"
print("아뇨, {}인데요?".format(a))
```
