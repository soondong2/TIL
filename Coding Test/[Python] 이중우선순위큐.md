# Today I Learned - 2023/05/21

## 이중우선순위큐
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/42628
- 난이도 : Level3

## 풀이
```python
from heapq import heappop, heappush, heapify

def maxheap(heapq):
    heap = []
    max_heap = []
    for h in heapq:
        h = int(h)
        heappush(heap, (-h, h))
    
    while heap:
        max_heap.append(heappop(heap)[1])

    return max_heap

                
def solution(operations):
    heap = []
    for o in operations:
        string, num = o.split()[0], int(o.split()[1])
        
        if string == 'I':
            heappush(heap, num)
        elif string == 'D' and num == 1 and len(heap) > 0:
            heap = maxheap(heap)
            heappop(heap)
        elif string == 'D'and num == -1 and len(heap) > 0:
            heappop(heap)
        elif len(heap) == 0:
            pass
        
    if len(heap) == 0:
        return [0, 0]
    else:
        return [max(heap), min(heap)]
```
