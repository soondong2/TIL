# Today I Learned - 2022/10/13 Thur

# 올바른 괄호
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/12909
- 난이도 : Level2
<br>

## 풀이
```python
from collections import deque

def solution(parseq):
    answer = True
    stack = deque()
    for p in parseq:
        if p == "(":
            stack.append(p)
        elif p == ")":
            if len(stack) == 0:
                return False
            else:
                stack.pop()
        else:
            print("Not allwed symbol")

    if len(stack) > 0:
        return False
    else:
        return answer
```
