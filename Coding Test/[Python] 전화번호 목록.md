# Today I Learned - 2022/10/25 Tue

# 전화번호 목록
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/42577
- 난이도 : Level2
<br>

## 풀이
### Hash 사용
```python
def solution(phone_book):
    # 1. Hash map을 만든다
    hash_map = {}
    for phone_number in phone_book:
        hash_map[phone_number] = 1
        
    # 2. 접두어가 Hash map에 존재하는지 찾는다
    for phone_number in phone_book:
        jubdoo = ""
        for number in phone_number:
            jubdoo += number
            # 3. 접두어를 찾아야 한다 (기존 번호와 같은 경우 제외)
            if jubdoo in hash_map and jubdoo != phone_number:
                return False
    return True
```
- 정확성: 83.3
- 효율성: 16.7
