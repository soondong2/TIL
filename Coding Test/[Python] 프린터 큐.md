# Today I Learned - 2023/05/19

## 1996번: 프린터 큐
- 출처 : https://www.acmicpc.net/problem/1966
- 난이도 : Silver3

## 풀이
```python
from collections import deque

t = int(input())

for i in range(t):
    answer = 0
    n, m = map(int, input().split())
    prioties = list(map(int, input().split()))

    prioty = [(i, p) for i, p in enumerate(prioties)]
    queue = deque(prioty)

    while queue:
        temp = queue.popleft()
        if any(temp[1] < q[1] for q in queue):
            queue.append(temp)
        else:
            answer += 1
            if temp[0] == m:
                print(answer)
```
