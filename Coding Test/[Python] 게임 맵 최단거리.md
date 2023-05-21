# Today I Learned - 2023/05/21

## 타겟 넘버
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/1844
- 난이도 : Level2

## 풀이
```python
from collections import deque

def solution(maps):
    answer = 0
    
    # 상하좌우
    dx = [-1, 1, 0, 0]
    dy = [0, 0, -1, 1]
    
    def bfs(x, y):
        queue = deque()
        queue.append((x, y))

        while queue:
            x, y = queue.popleft()
            
            # 상하좌우 칸 확인
            for i in range(4):
                nx = x + dx[i]
                ny = y + dy[i]
                
                # 맵 벗어나면 무시
                if nx < 0 or ny < 0 or nx >= len(maps) or ny >= len(maps[0]): 
                    continue
                # 벽 무시
                if maps[nx][ny] == 0:
                    continue
                # 처음 방문하는 곳 거리 계산, 재귀 호출
                if maps[nx][ny] == 1:
                    maps[nx][ny] = maps[x][y] + 1
                    queue.append((nx, ny))
                    
        # 거리 반환
        return maps[len(maps) - 1][len(maps[0]) - 1]

    answer = bfs(0, 0)
    
    # 상대 팀 진영에 도착할 수 없을 때는 -1
    if answer == 1:
        return -1
    else:
        return answer
```
