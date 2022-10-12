# Today I Learned - 2022/10/12 Wed

# 큐(Queue)
- `FIFO` : (First In First Out)
- `enqueue` : 어느 인덱스로 들어와야 하는지 -> list의 append 사용
- `dequeue` : 다음에 나갈 값이 어느 인덱스에 있는지 -> front_index
<br>

>스택과 큐의 차이점

||Insert|Delete|
|:---:|:---:|:---:|
|Stack|Push|Pop|
|Queue|Enqueue|Dequeue|
<br>

## 큐
```python
class Queue:
  def __init__(self):
    self.items = []  # 빈 리스트 생성
    self.front_index = 0  # 인덱스 위치 확인을 위해 초기화
    
  def enqueue(self, value):  # 삽입
    self.items.append(value)
  
  def dequeue(self):  # 삭제
    if self.front_index == len(self.items):  # front_index의 위치와 len(Queue)의 수가 같다면 Queue는 비어있는 상태
      print("Q is empty")
      return None
      
    else:
      x = self.items[self.front_index]  # list[index]로 찾은 값을 x에 지정
      self.front_index += 1  # dequeue 될 때마다 front_index + 1
      return x
```
<br>

## 요세푸스(Josephus Problem)
```python
from collections import deque

n, k = map(int, input().split())
queue = deque([i for i in range(1, n+1)])

m = 1
result = []
while queue:
    if m % k == 0:
        result.append(queue.popleft())
        m += 1

    else:
        queue.append(queue.popleft())
        m += 1

print(result)
```
<br>

# deque
- deque를 사용하는 이유는 양방향 큐 방식을 활용할 수 있으며, 리스트보다 속도가 빠르다.
<br>

## Method
|Method|설명|
|:---:|:---:|
|q.append(item)|오른쪽 끝에 삽입|
|q.appendleft(item)|왼쪽 끝에 삽입|
|q.pop()|가장 오른쪽 요소 반환 및 삭제|
|q.popleft()|가장 왼쪽 요소 반환 및 삭제|
|q.extend(array)|주어진 배열을 순회하며 q의 오른쪽에 추가|
|q.extendleft(array)|주어진 배열을 순회하며 q의 왼쪽에 추가|
|q.remove(item)|삭제|
|q.rotate(숫자)|해당 숫자만큼 회전(양수 : 시계방향, 음수 : 반시계방향|

