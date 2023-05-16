# Today I Learned - 2023/05/16

## 10773번: 제로
- 출처 : https://www.acmicpc.net/problem/10773
- 난이도 : Silver4

## 풀이
```python
from collections import deque

k = int(input())
stack = deque()
for _ in range(k):
    num = int(input())
    if num == 0:
        stack.pop()
    else:
        stack.append(num)

print(sum(stack))
```
