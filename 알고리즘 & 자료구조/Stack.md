# Today I Learned - 2022/10/11 Tue

# 스택(Stack)
- 제한된 접근(삽입, 삭제)만 허용한다.
- `LIFO` : Last In First Out, 마지막에 들어온 게 먼저 나간다.

## 기본 스택 구현
```python
class Stack:
  def __init__(self):  # 생성함수, Stack 이라는 객체를 생성
    self.items = []    # 데이터 저장을 위한 빈 리스트 생성
    
  def push(self, val):  # 삽입
    self.items.append(val)
    
  def pop(self):  # 삭제
    try:
      return self.items.pop()
    except IndexError:
      print("Stack is empty")
      
  def top(self):  # Stack의 가장 위에 있는 값을 return
    try:
      return self.items[-1]
    except IndexError:
      print("Stack is empty")
      
  def __len__(self):  # len()을 호출하면 Stack의 item의 수를 반환
    return len(self.items)
```
<br>

## 괄호 맞추기
- 입력 : 왼쪽, 오른쪽 괄호의 문자열
- 출력 : 괄호 쌍이 맞으면 True, 아니면 False
- 왼쪽 괄호는 나의 쌍이 나타날 때까지 Stack에서 대기한다.
<br>

```python
S = Stack()
parseq = "괄호 입력하기"

def stack(parseq):
    for p in parseq:
        if p == "(":
            S.push(p)
        elif p == ")":
            if len(S.items) == 0:
                print("False")
                exit(0)
            else:
                S.pop()
        else:
            print("Not alllwed symbol")

    if len(S) > 0:
        print("False")
    else:
        print("True")

stack(parseq)
```
