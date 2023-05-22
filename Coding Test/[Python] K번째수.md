# Today I Learned - 2023/05/22

## K번째수
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/42748
- 난이도 : Level1

## 풀이
```python
def solution(array, commands):
    answer = []
    for c in commands:
        answer.append(sorted(array[c[0] - 1 : c[1]])[c[2] - 1])
    return answer
```
