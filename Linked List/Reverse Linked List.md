## [Reverse Linked List]

### 1. 문제 요약
주어진 단일 연결 리스트의 모든 노드들의 순서를 거꾸로 뒤집는 문제

### 2. 초기 접근 및 풀이

#### 초기 코드
```python
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        # 1. 세 개의 포인터를 준비합니다.
        prev = None          # 이전 노드를 가리킬 포인터
        curr = head          # 현재 노드를 가리킬 포인터
        
        # 2. 현재 노드가 None이 될 때까지 (리스트 끝에 도달할 때까지) 반복합니다.
        while curr:
            # 3. 다음 노드를 미리 저장해 둡니다. (연결이 끊기기 전에)
            next_temp = curr.next
            
            # 4. 현재 노드의 화살표(next) 방향을 이전 노드(prev)로 뒤집습니다.
            curr.next = prev
            
            # 5. 두 포인터를 다음 작업을 위해 한 칸씩 앞으로 이동시킵니다.
            prev = curr
            curr = next_temp
            
        # 6. 루프가 끝나면 prev는 뒤집힌 리스트의 새로운 head가 됩니다.
        return prev
```


### 3. 핵심 정리 및 주요 원칙

#### 핵심 정리
세 개의 포인터(prev, curr, next_temp)를 사용하여 리스트를 한 번만 순회하면서, 현재 노드(curr)의 next 포인터가 이전 노드(prev)를 가리키도록 방향을 차례대로 뒤집는 것

#### 주요 원칙

1. 세 개의 포인터 활용: 각자 명확한 역할을 가진 세 개의 포인터를 사용합니다.

    - prev: 뒤집힌 리스트의 현재 머리 부분을 가리킵니다. (초기값: None)

    - curr: 현재 방향을 뒤집어야 할 대상 노드를 가리킵니다. (초기값: head)

    - next_temp: curr의 포인터 방향을 바꾸기 전에, 원래의 다음 노드를 임시로 저장하여 연결이 끊어지는 것을 방지합니다.

2. 반복적인 포인터 재연결: while 루프 안에서 다음 세 가지 동작을 반복합니다.

    - 저장: next_temp = curr.next

    - 뒤집기: curr.next = prev

    - 이동: prev = curr, curr = next_temp

3. 연결고리 보존: next_temp 포인터의 역할이 매우 중요합니다. curr.next의 방향을 바꾸는 순간 원래의 다음 노드로 갈 방법이 사라지므로, 이 포인터에 미리 다음 노드를 저장해두어야 합니다.
