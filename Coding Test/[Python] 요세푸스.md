# Today I Learned - 2023/05/15

## 1158번: 요세푸스
- 출처 : https://www.acmicpc.net/problem/1158
- 난이도 : Silver4

## 풀이
```python
from collections import deque

n, k = map(int, input().split())
people = list(range(1, n + 1))
stack = deque(people)

answer = []
while stack:
    stack.rotate(-(k - 1))
    temp = stack.popleft()
    answer.append(temp)

print('<', ', '.join(str(a) for a in answer), '>', sep='')
```
