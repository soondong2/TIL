# Today I Learned - 2022/11/30 Wed

# 캐릭터의 좌표
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/120861
- 난이도 : Level0

```python
def solution(keyinput, board):
    x = board[0]  
    y = board[1]  
    
    answer = [0, 0]
    
    for k in keyinput:
        if k == 'left' and answer[0]-1 >= -(x // 2):
            answer[0] -= 1 
        elif k == 'right' and answer[0]+1 <= (x // 2):
            answer[0] += 1
        elif k == 'up' and answer[1]+1 <= (y // 2):
            answer[1] += 1
        elif k == 'down' and answer[1]-1 >= -(y // 2):
            answer[1] -= 1
        
    return answer
```
