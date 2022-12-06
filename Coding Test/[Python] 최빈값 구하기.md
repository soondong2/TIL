# Today I Learned - 2022/12/06 Tue

# 최빈값 구하기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/120812
- 난이도 : Level0
<br>

## 풀이
```python
def solution(array):
    array_dict = {}
    for a in array:
        if a not in array_dict.keys():
            array_dict[a] = 1
        else:
            array_dict[a] += 1
    
    keys = list(array_dict.keys())
    values = list(array_dict.values())

    if values.count(max(values)) <= 1:
        answer = keys[values.index(max(values))]
    else:
        answer = -1
    return answer
```
