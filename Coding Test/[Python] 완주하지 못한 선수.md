# Today I Learned - 2022/10/25 Tue

# 완주하지 못한 선수
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/42576
- 난이도 : Level1
<br>

## 풀이
```python
def solution(participant, completion):
    participant.sort()
    completion.sort()

    for p, c in zip(participant, completion):
        if p != c:
            return p
    return participant.pop()
```
<br>

- `zip(a, b)` : 배열을 같은 인덱스끼리 짝지어준다. 만약 배열의 길이가 다를 경우 같은 인덱스끼리만 짝지어주고, zip 객체에서 나머지 인덱스는 제외된다.
