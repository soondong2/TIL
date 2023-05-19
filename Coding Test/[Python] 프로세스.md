# Today I Learned - 2023/05/19

# 프로세스
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/42587
- 난이도 : Leve2

## 풀이
```python
from collections import deque

def solution(priorities, location):
    answer = 0
    prosess = [(i, p) for i, p in enumerate(priorities)]
    queue = deque(prosess)
    
    while queue:
        temp = queue.popleft()
        if any(temp[1] < q[1] for q in queue):
            queue.append(temp)
        else:
            answer += 1
            if temp[0] == location:
                return answer
```
