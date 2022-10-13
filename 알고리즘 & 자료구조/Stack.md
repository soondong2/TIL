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

## 1. 괄호 맞추기
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
            print("Not allowed symbol")

    if len(S) > 0:
        print("False")
    else:
        print("True")

stack(parseq)
```

<br>

### deque를 활용한 stack
```python
from collections import deque

parseq = "()("
def solution(parseq):
    stack = deque()
    for p in parseq:
        if p == "(":
            stack.append(p)
        elif p == ")":
            if len(stack) == 0:
                return False
            else:
                stack.pop()
        else:
            print("Not allwed symbol")

    if len(stack) > 0:
        return False
    else:
        return True

print(solution(parseq))
```

<br>

## 계산기 코드
### ifix 수식 -> postfix 수식
1) 괄호 치기
2) 해당 연산자의 오른쪽 괄호 다음으로 연산자를 이동
3) 괄호 지후기
<br>

```python
S = Stack()
outstack = []

tokens = list(map(str, input().strip()))  # 입력 받기
prior = {'*': 3, '/': 3, '+': 2, '-': 2, '(': 1}  # 연산자 우선순위 지정

for t in tokens:
    if t.isdigit():  # 피연산자는 바로 outstack에 추가
        outstack.append(t)

    elif t == '(':  # '(' 가 나타나면 Stack에 추가
        S.push(t)

    elif t == ')':
        while S.top() != '(':  # '(' 가 나타나기 전까지 반복
            outstack.append(S.pop())  # Stack에 담겨 있는 연산자 pop 처리 및 outstack에 담기
        S.pop()  # '('가 나타나면 pop 처리

    else:  # 그 외 t가 Stack[-1]의 우선순위와 같거나 작으면 t의 우선순위가 커질 때까지 pop
        while S and prior[t] <= prior[S.top()]:
            outstack.append(S.pop())
        S.push(t)

while len(S) != 0:  # Stack에 남아있는 연산자들 outstack에 추가
    outstack.append(S.pop())

print(outstack)
```
<br>

### 계산하기
```python
stack = []   # 피연산자 바로 추가할 리스트 생성
a = 0   # stack[-1]을 위한 변수 생성
b = 0  # stack[-2]을 위한 변수 생성

for l in range(len(outstack)):   # 후위표기법으로 저장되 있는 리스트의 수만큼 반복
    if outstack[l].isdigit():    # 만약 피연산자이면 바로 stack에 추가
        stack.append(int(outstack[l]))
    elif outstack[l] == '+': # + 이면 stack에서 2개 피연산자를 pop하여 게산해준뒤 다시 stack에 추가
        a = stack.pop()
        b = stack.pop()
        stack.append(b + a)
    elif outstack[l] == '-': # - 이면 stack에서 2개 피연산자를 pop하여 게산해준뒤 다시 stack에 추가
        a = stack.pop()
        b = stack.pop()
        stack.append(b - a)
    elif outstack[l] == '*': # * 이면 stack에서 2개 피연산자를 pop하여 게산해준뒤 다시 stack에 추가
        a = stack.pop()
        b = stack.pop()
        stack.append(b * a)
    elif outstack[l] == '/': # / 이면 stack에서 2개 피연산자를 pop하여 게산해준뒤 다시 stack에 추가
        a = stack.pop()
        b = stack.pop()
        stack.append(b / a)

print(stack)
```
