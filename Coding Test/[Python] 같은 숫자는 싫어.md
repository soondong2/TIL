# Today I Learned - 2022/10/12 Wed

# 같은 숫자는 싫어
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/12906
<br>

## 풀이
```python
def solution(arr):
    answer = []
    for i in arr:
        answer.append(i)
        if len(answer) >= 2 and answer[-1] == answer[-2]:
            answer.pop()
            
    return answer
```
