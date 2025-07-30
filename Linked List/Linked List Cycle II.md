## Linked List Cycle II

### 1. 문제 요약
연결 리스트에서 사이클이 존재하는지 확인하고, 사이클이 있다면 사이클이 시작되는 노드를 찾아 반환하는 문제입니다.

### 2. 초기 접근 및 풀이

#### 핵심 로직
(처음 떠올렸던 아이디어를 순서대로 작성합니다.)

#### 초기 코드
```python
class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        slow = head
        fast = head
        
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            
            if slow == fast:
                finder = head
                while finder != slow:
                    finder = finder.next
                    slow = slow.next

                return finder
            
        return None
```

#### 복잡도 분석

- 시간 복잡도:
- 공간 복잡도:

### 3. 피드백 및 개선점
(내 풀이의 비효율적인 부분이나 개선할 점을 작성합니다.)

### 4. 최적화된 풀이

#### 개선된 로직
(개선된 아이디어를 작성합니다.)

#### 최종 코드

```python
# 여기에 최종 코드를 붙여넣습니다.
```

#### 복잡도 분석

- 시간 복잡도:
- 공간 복잡도:

### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리
(이 문제를 통해 배운 핵심 교훈을 한 문장으로 정리합니다.)

#### 주요 원칙
(문제를 풀며 깨달은 자신만의 원칙이나 데이터 순회 규칙 등을 기록합니다.) 