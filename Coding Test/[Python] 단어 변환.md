# Today I Learned - 2023/05/26

## 단어 변환
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/43163
- 난이도 : Level3

## 풀이
```python
from collections import deque

def solution(begin, target, words):
    answer = 0
    
    queue = deque()
    queue.append([begin, 0])
    
    visited = [False for i in range(len(words))]
    
    while queue:
        word, cnt = queue.popleft()
        if word == target:
            answer = cnt
            break
        
        for i in range(len(words)):
            temp = 0
            if visited[i] == False:
                for j in range(len(word)):
                    if word[j] != words[i][j]:
                        temp += 1
                if temp == 1:
                    queue.append([words[i], cnt + 1])
                    visited[i] = True

    return answer
```
