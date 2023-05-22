# Today I Learned - 2023/05/22

## K번째수
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/43164
- 난이도 : Level3

## 풀이
```python
from collections import defaultdict

def solution(tickets):
    answer = []
    
    # {start:[end1, end2, ...]}
    graph = defaultdict(list)
    for start, end in tickets:
        graph[start].append(end)
    
    # 도착치 알파벳 오름차순 정렬
    for start in graph.keys():
        graph[start].sort(reverse=True)
    
    stack = ['ICN']
    while stack:
        top = stack.pop()
        # top 경로로 출발하고 다른 경로로 도착하는 경우가 없을 경우
        if top not in graph or len(graph[top]) == 0:
            answer.append(top)
        # 남은 경로가 있을 경우
        else:
            stack.append(top)
            stack.append(graph[top].pop())
            
    return answer[::-1]
```
