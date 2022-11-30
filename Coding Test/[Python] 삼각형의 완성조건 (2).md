# Today I Learned - 2022/11/30 Wed

# 삼각형의 완성조건 (2)
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/120868
- 난이도 : Level0
<br>

## 풀이
```python
def solution(sides):
    answer1 = list(range(max(sides) - min(sides) + 1, max(sides)+1))
    answer2 = list(range(max(answer1)+1, sum(sides)))
    
    answer = len(answer1) + len(answer2)
    return answer
```
