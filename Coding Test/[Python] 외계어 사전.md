# Today I Learned - 2022/11/29 Tue

# 외계어 사전
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/120869
- 난이도 : Level0
<br>

## 풀이
```python
def solution(spell, dic):
    for d in dic:
        if set(spell).issubset(d):
            return 1
    return 2
```
