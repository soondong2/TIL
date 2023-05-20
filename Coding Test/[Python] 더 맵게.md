# Today I Learned - 2023/05/20

## 더 맵게
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/42626
- 난이도 : Level2

## 풀이
```python
from heapq import heappush, heappop, heapify

def solution(scoville, K):
    answer = 0
    heapify(scoville)
    
    while scoville[0] < K:
        try:
            first = heappop(scoville)
            second = heappop(scoville)

            new = first + (second * 2)
            heappush(scoville, new)
            
            answer += 1
        except:
            return -1
    return answer
```
