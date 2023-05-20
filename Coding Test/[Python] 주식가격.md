# Today I Learned - 2023/05/20

## 주식가격
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/42584
- 난이도 : Level2

## 풀이
```python
from collections import deque

def solution(prices):
    answer = []
    stack = deque(prices)
    
    while stack:
        temp = stack.popleft()
        cnt = 0
        for s in stack:
            cnt += 1
            if temp > s:
                break
        answer.append(cnt)
                
    return answer
```
