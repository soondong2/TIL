# Today I Learned - 2022/10/24 Mon

# 기능개발
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/42586
- 난이도 : Leve2
<br>

## 풀이
```python
def solution(progresses, speeds):
    answer = []

    while progresses:
        for i in range(len(progresses)):
            progresses[i] += speeds[i]

        cnt = 0
        while progresses and progresses[0] >= 100:
            progresses.pop(0)
            speeds.pop(0)
            cnt += 1

        if cnt > 0:
            answer.append(cnt)

    return answer
```
