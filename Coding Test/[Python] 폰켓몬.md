# Today I Learned - 2022/10/25 Tue

# 폰켓몬
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/1845
- 난이도 : Level1
<br>

## 풀이
```python
def solution(nums):
    choice = int(len(nums) / 2)  # 가져갈 수 있는 개수
    answer = int(len(set(nums)))  # 중복 제거한 개수

    if answer >= choice:
        return choice
    return answer
```
