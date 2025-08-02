## [Remove Nth Node From End of List]

### 1. 문제 요약

연결 리스트와 숫자 n이 주어질 때, 리스트의 끝에서 n번째에 있는 노드를 삭제하고, 수정된 리스트의 시작점(head)을 반환하는 문제

### 2. 초기 접근 및 풀이

#### 핵심 로직

- 더비 노드를 만든다.
- 포인터 두개를 만들어 하나는 미리 n번째 칸에 위치시킨다.
- 그리고 나서 두 포인터를 앞선 포인터 끝까지 위치한다면, 느린 포인터는 뒤에서 n번째 앞에 위치할 것.

#### 초기 코드
```python
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode(0, head)
        slow = dummy
        fast = dummy
        
        for _ in range(n + 1):
            fast = fast.next
            
        while fast:
            slow = slow.next
            fast = fast.next
            
        slow.next = slow.next.next
        
        return dummy.next
```

### 3. 핵심 정리 및 주요 원칙

#### 핵심 정리

두 개의 포인터(slow, fast)를 n만큼의 간격을 두고 함께 움직이는 것

#### 주요 원칙

1. 투 포인터와 간격 유지: fast 포인터를 slow 포인터보다 n칸 만큼 먼저 앞으로 보내, 두 포인터 간의 상대적인 거리를 일정하게 유지하며 탐색합니다.

2. 더미 노드(Dummy Node) 활용: 리스트의 맨 앞(head) 노드를 삭제해야 하는 예외적인 경우를 깔끔하게 처리하기 위해, 실제 head 앞에 가짜 노드를 두어 slow 포인터가 항상 삭제할 노드의 '이전 노드'를 가리킬 수 있도록 보장합니다.

3. 동시 전진: 간격을 설정한 후에는, fast 포인터가 리스트의 끝에 닿을 때까지 두 포인터를 같은 속도로 함께 전진시켜 목표 위치를 찾습니다.