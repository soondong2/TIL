# Today I Learned - 2022/12/05 Mon

# 등수 매기기
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/120882
- 난이도 : Level0
<br>

## 풀이
```python
def solution(score):
    s_mean = sorted([sum(s) / 2 for s in score], reverse=True)
    rank_dict = {}
    
    for i, s in enumerate(s_mean):
        if s not in rank_dict.keys():
            rank_dict[s] = i + 1
    
    answer = [rank_dict[sum(s) / 2] for s in score]
    return answer
```
