# Today I Learned - 2023/05/20

## 타겟 넘버
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/43165
- 난이도 : Level2

## 풀이
```python
from itertools import product

def solution(numbers, target):
    data = [[-n, n] for n in numbers]
    answer = list(map(sum, product(*data))).count(target)
    return answer
```
