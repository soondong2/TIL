# Today I Learned - 2022/05/09 Mon

## 📌 반복문
### while문
무한루프에 걸리게 되므로 `If`문이나 `break` 를 이용하여 무한루프에서 빠져나온다.
- `continue`
- `pass`
```python
i = 0
while True:
  print(i)
  i += 1
```
```python
i = 0
while True:
  if i >= 3:
    break
  else:
    print(i)
```

### for문
- 변수 `i`에 0, 1, 2, 3, 4가 차례대로 담긴다.
- 파이썬은 `0`부터 시작함에 주의한다.
- `range(시작, 끝, 간격)`으로 사용하며 숫자 하나만 입력시 `range(끝)`와 같다.
- ex) range(5)는 0부터 5 - 1 = 4까지를 의미한다.
```python
for i in range(5):
  print(i + 1)
```

- `_`는 변수에 담지 않고 range(3)만큼 print문을 반복한다는 의미이다.
```python
for _ in range(3):
  print("Hello")
```
