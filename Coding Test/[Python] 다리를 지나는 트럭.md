# Today I Learned - 2023/05/20

## 다리를 지나는 트럭
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/42583
- 난이도 : Level2

## 풀이
```python
def solution(bridge_length, weight, truck_weights):
    time = 0
    queue = [0] * bridge_length
    bridge_sum = sum(queue)
    
    while queue:
        time += 1
        bridge_sum -= queue.pop(0)
        if truck_weights:
            if bridge_sum + truck_weights[0] <= weight:
                bridge_sum += truck_weights[0]
                queue.append(truck_weights.pop(0))
            else:
                queue.append(0)
            
    return time
```

## 시간 초과 문제 해결
제출 시 테스트 케이스 5번에 대해서 시간 초과 문제가 발생했다. deque를 사용해도 시간 초과가 발생했다. 기존 코드에는 `bridge_sum = sum(queue)` 코드가 없었으며, 다리 위의 무게를 계산하는 코드를 `sum()`을 활용했다. 해당 부분에서 시간 초과가 발생하였기에 다리 위 무게를 변수로 담고 sum을 사용하지 않는 방법으로 해결했다.
