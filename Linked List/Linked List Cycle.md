## [Linked List Cycle]

### 1. 문제 요약

주어진 연결 리스트에 순환(사이클) 구간이 존재하는지 판별하는 문제입니다. 만약 사이클이 있다면 True를, 없다면 False를 반환해야 하는 문제.

### 2. 초기 접근 및 풀이

#### 핵심 로직

앞서 배웠던 토끼와 거북이 알고리즘을 적용하면 쉽게 풀 수 있다.

#### 초기 코드

```python
class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        if not head or not head.next:
            return False
        
        slow = head
        fast = head
        
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            
            if slow == fast:
                return True
            
        return False
```


### 4. 핵심 정리 및 주요 원칙

#### 핵심 정리

속도가 다른 두 개의 포인터(느린 '거북이'와 빠른 '토끼')를 연결 리스트 위에서 동시에 출발시켜, 두 포인터가 서로 만나게 되면 사이클이 존재한다고 판별하는 것

#### 주요 원칙

1. 투 포인터 (토끼와 거북이 알고리즘): 이 문제 해결의 핵심 기법입니다.

    - slow 포인터 (거북이): 한 번에 한 칸씩 이동합니다. (slow = slow.next)
    - fast 포인터 (토끼): 한 번에 두 칸씩 이동합니다. (fast = fast.next.next)

2. 만남으로 사이클 판별: 만약 리스트에 사이클이 존재한다면, 더 빠른 fast 포인터가 사이클 안에서 결국 slow 포인터를 따라잡아 같은 노드를 가리키는 순간이 반드시 오게 됩니다. 이 "만남"이 바로 사이클의 존재 증거입니다.

3. 종료 조건 (사이클이 없는 경우): 만약 사이클이 없다면, fast 포인터(또는 fast.next)가 먼저 리스트의 끝(None)에 도달하게 됩니다. 루프가 이 조건 때문에 종료되었다면, 이는 사이클이 없다는 것을 의미합니다.

4. 상수 공간 복잡도 (O(1)): 이 알고리즘은 추가적인 자료구조(예: set)를 사용하지 않고 단 두 개의 포인터 변수만으로 문제를 해결하므로, 메모리 사용량이 매우 효율적입니다.