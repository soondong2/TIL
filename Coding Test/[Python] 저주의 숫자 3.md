# Today I Learned - 2022/12/08 Thur

# 저주의 숫자 3
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/120871
- 난이도 : Level0
<br>

## 풀이
```python
def solution(n):
    i = 1
    num = []
    while len(num) < 101:
        if '3' not in str(i) and i % 3 != 0:
            num.append(i)
            i += 1
        else:
            i += 1
    answer = num[n - 1]
    return answer
```
