# Today I Learned - 2022/10/13 Thur

# 괄호
- 출처 : https://www.acmicpc.net/problem/9012
- 난이도 : Silver4
<br>

## 풀이
```python
from collections import deque
import sys

N = int(sys.stdin.readline())

for i in range(N):
    parseq = list(sys.stdin.readline())[:-1]

    stack = deque()
    for p in parseq:
        if p == "(":
            stack.append(p)
        elif p == ")":
            if len(stack) == 0:
                result = "NO"
                break

            else:
                stack.pop()
        else:
            print("Not allwed symbol")

        if len(stack) > 0:
            result = "NO"
        else:
            result = "YES"

    print(result)
```
