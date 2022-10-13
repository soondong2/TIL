# Today I Learned - 2022/10/13 Tur

# 연결 리스트(Linked List)
- `노드(node)`와 `링크(link)`로 연결된 구조를 연결 리스트(Linked List)라고 한다.
- 장점
  - 삽입과 삭제가 상수 시간 O(1)에 이루어진다.
  - 메모리 관리가 용이하다.
- 단점 : 배열처럼 index를 통한 탐색이 불가능하다.
<br>

## 시간 복잡도
||Array|Linked List|
|:---:|:---:|:---:|
|삽입|O(N)|O(1)|
|삭제|O(N)|O(1)|
|탐색|O(1)|O(n)|
<br>

## 단일 연결 리스트(Singly Linked List)
### Push Front, Push Back
```python
# 단일 연결 리스트
class SinglyLinkedList:
  # Node 생성
  class _Node:
    def __init__(self, element=None, next=None):
      self._element = element
      self._next = next

    def __str__(self):
      return str(self._element)

  def __init__(self):
    self._head = None
    self._tail = None
    self._size = 0

  def __len__(self):
    return self._size

  def add_first(self, element):
    newest = self._Node(element, self._head)  # 새 노드 생성 self._head = newest
      self._head = newest
      self._size += 1

  def add_last(self, element):
    newest = self._Node(element)
      if self._head is None:
        self.add_first(element)
      else:
        tail = self._head
        while tail._next is not None:
          tail = tail._next
        tail._next = newest
        self._size += 1

  def pop_first(self):
        if self._head is None:
            return None
        element = self._head
        self._head = self._head._next
        self._size -= 1
        return element

  def pop_last(self):
    if self._head is None:
      return None
    tail = self._head
    prev = None
    while tail._next is not None:
      prev = tail
      tail = tail._next
        
    # 루프를 탈출하면 tail은 마지막 노드, prev는 그 이전 노드를 가리킴
    # 만일 리스트의 요소가 하나라면 반복문을 수행하지 않음
    if prev is None:
      self._head = None
    else:
      prev._next = None
    self._size -= 1
    return tail._element
```
