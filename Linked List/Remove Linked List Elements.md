## Remove Linked List Elements

### 1. 문제 요약
연결 리스트와 특정 값 val이 주어질 때, 리스트에서 값이 val과 일치하는 모든 노드를 삭제하고, 수정된 리스트의 시작점(head)을 반환하는 문제

### 2. 초기 접근 및 풀이

#### 초기 코드
```python
class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        # 1. 더미 노드를 생성하고, 실제 head 앞에 연결합니다.
        #    이렇게 하면 head를 삭제해야 하는 경우를 쉽게 처리할 수 있습니다.
        dummy = ListNode(0, head)
        
        # 2. 두 개의 포인터를 준비합니다.
        #    prev는 삭제되지 않는 마지막 노드를 가리킵니다.
        #    curr는 현재 확인 중인 노드를 가리킵니다.
        prev = dummy
        curr = head
        
        # 3. 리스트의 끝에 도달할 때까지 순회합니다.
        while curr:
            # 4. 현재 노드의 값이 삭제해야 할 값(val)과 같은 경우
            if curr.val == val:
                # prev의 next 포인터를 현재 노드(curr)를 건너뛰고
                # 다음 노드(curr.next)를 가리키게 하여 curr를 삭제합니다.
                prev.next = curr.next
            # 5. 현재 노드의 값이 val과 다른 경우 (삭제하지 않음)
            else:
                # prev를 현재 노드로 한 칸 이동시킵니다.
                prev = curr
            
            # 6. curr를 다음 노드로 이동시켜 계속 탐색합니다.
            curr = curr.next
            
        # 7. 더미 노드의 다음 노드가 바로 수정된 리스트의 새로운 시작점입니다.
        return dummy.next
```

### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리
실제 head 앞에 '더미 노드(dummy node)'를 두어, prev 포인터가 항상 삭제할 노드의 '이전 노드'를 가리킬 수 있도록 보장한 뒤, 리스트를 순회하며 삭제할 값을 가진 노드를 '건너뛰도록' 포인터를 재연결하는 것

#### 주요 원칙
1. 더미 노드(Dummy Node) 활용: 리스트의 맨 앞(head) 노드를 삭제해야 하는 예외적인 경우를 일반적인 경우와 동일한 로직으로 처리하기 위해 사용합니다. 이는 코드의 복잡성을 크게 낮춰줍니다.

2. '이전' 포인터(prev) 유지: 노드를 삭제하려면 그 노드의 바로 이전 노드를 알아야 합니다. prev 포인터는 현재 노드(curr)를 따라가며, 삭제되지 않는 마지막 노드의 위치를 계속 추적하는 중요한 역할을 합니다.

3. '건너뛰기'를 통한 삭제: 노드를 실제로 메모리에서 지우는 것이 아니라, prev.next = curr.next 와 같이 prev 포인터가 삭제할 curr 노드를 건너뛰고 다음 노드를 가리키게 함으로써 연결고리에서 제외하는 방식으로 삭제를 구현합니다.
