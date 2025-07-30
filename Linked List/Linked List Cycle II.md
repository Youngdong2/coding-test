## Linked List Cycle II

### 1. 문제 요약
연결 리스트에서 사이클이 존재하는지 확인하고, 사이클이 있다면 사이클이 시작되는 노드를 찾아 반환하는 문제.

### 2. 초기 접근 및 풀이

#### 핵심 로직
- 해시 셋을 이용해 방문했던 노드들을 저장한다.
- 한칸씩 전진하면서 방문 여부를 확인한다.
- 만약 사이클이 없는 경우 언젠가는 리스트의 끝에 도달하게 된다.

#### 초기 코드
```python
class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        seen_nodes = set()
        
        current = head
        while current:
            if current in seen_nodes:
                return current
            
            seen_nodes.add(current)

            current = current.next
        
        return None
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(N)


### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리
연결 리스트를 순회하면서, 방문하는 모든 노드를 해시 셋(Hash Set)에 기록하고, 만약 이미 기록된 노드를 다시 만나게 되면 바로 그 노드가 사이클의 시작점이라고 판별하는 것

#### 주요 원칙
해시 셋을 이용한 방문 기록: set 자료구조를 '방문 기록부'로 사용하여, 각 노드를 방문했는지 여부를 O(1)의 빠른 속도로 확인합니다.

선형 탐색 (Linear Scan): 리스트의 head부터 next 포인터를 따라 한 번만 순회하여 문제를 해결합니다.

최초의 중복이 곧 시작점: 이 방식에서는 순환 구간 내에서 처음으로 중복 발견되는 노드가 곧 사이클의 시작점이 됩니다. 이는 플로이드 알고리즘처럼 2단계에 걸친 추가 계산이 필요 없어 로직이 매우 직관적입니다.