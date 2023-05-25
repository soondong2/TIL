# Today I Learned - 2023/05/25

## 네트워크
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/43162
- 난이도 : Level3

## 풀이
### DFS
```python
def dfs(n, computers, visited, i):
    visited[i] = True
    
    for j in range(n):
        if i != j and computers[i][j] == 1:
            if visited[j] == False:
                dfs(n, computers, visited, j)
        
def solution(n, computers):
    answer = 0
    visited = [False for i in range(n)]
    
    for i in range(n):
        if visited[i] == False:
            dfs(n, computers, visited, i)
            answer += 1
            
    return answer
```
