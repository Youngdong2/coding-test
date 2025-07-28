## Design Linked List

### 1. 문제 요약
연결 리스트 클래스를 직접 설계하고, 특정 위치의 값을 가져오거나 원하는 위치에 값을 추가하고 삭제하는 기본 기능들을 구현하는 문제


#### 핵심 로직

풀이의 핵심 포인트
- 더미 헤드(Dummy Head): 코드에서 self.head = ListNode()로 실제 데이터가 없는 '가짜 머리'를 하나 만들어두었습니다. 이렇게 하면 addAtHead나 deleteAtIndex(0)처럼 맨 앞 노드를 다뤄야 하는 복잡한 예외 케이스를, 다른 일반적인 경우와 똑같은 로직으로 처리할 수 있어 코드가 훨씬 단순해집니다.

- 이전 노드(prev) 찾기: 노드를 추가하거나 삭제할 때, 가장 중요한 것은 내가 원하는 위치의 **'바로 이전 노드'**를 찾는 것입니다. 이 이전 노드를 기준으로 next 포인터를 조작하여 연결고리를 바꾸는 것이 모든 연산의 핵심입니다.

- 크기(size) 관리: 노드를 추가할 때마다 self.size += 1, 삭제할 때마다 self.size -= 1을 해주어, 리스트의 현재 크기를 정확하게 추적하는 것이 중요합니다. 이는 get이나 addAtIndex 등에서 인덱스의 유효성을 검사할 때 필수적입니다.

#### 코드
```python
# 연결 리스트의 기본 단위가 되는 ListNode 클래스 정의
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val   # 노드가 저장하는 값
        self.next = next # 다음 노드를 가리키는 포인터

class MyLinkedList:

    def __init__(self):
        """
        연결 리스트를 초기화합니다.
        """
        # 더미 노드(dummy head)를 사용하면 맨 앞에 노드를 추가/삭제하는 등의
        # 예외 케이스를 더 쉽게 처리할 수 있습니다.
        self.head = ListNode() 
        self.size = 0 # 리스트에 있는 노드의 개수

    def get(self, index: int) -> int:
        """
        index 위치에 있는 노드의 값을 가져옵니다.
        index가 유효하지 않으면 -1을 반환합니다.
        """
        # 1. 인덱스가 유효한 범위인지 확인
        if index < 0 or index >= self.size:
            return -1
        
        # 2. head의 다음 노드부터 탐색 시작
        current = self.head.next
        # 3. 원하는 index에 도달할 때까지 한 칸씩 이동
        for _ in range(index):
            current = current.next
        
        return current.val

    def addAtHead(self, val: int) -> None:
        """
        리스트의 맨 앞에 새로운 노드를 추가합니다.
        """
        # addAtIndex(0, val) 함수를 재사용하면 코드가 간결해집니다.
        self.addAtIndex(0, val)

    def addAtTail(self, val: int) -> None:
        """
        리스트의 맨 뒤에 새로운 노드를 추가합니다.
        """
        # addAtIndex(self.size, val) 함수를 재사용합니다.
        self.addAtIndex(self.size, val)

    def addAtIndex(self, index: int, val: int) -> None:
        """
        index 위치에 새로운 노드를 추가합니다.
        index가 0이면 맨 앞에, index가 리스트 길이와 같으면 맨 뒤에 추가됩니다.
        index가 길이를 초과하면 아무것도 하지 않습니다.
        """
        # 1. 인덱스가 유효한 범위인지 확인 (맨 뒤에 추가하는 경우는 허용)
        if index < 0 or index > self.size:
            return
        
        # 2. 새로운 노드 생성
        new_node = ListNode(val)
        
        # 3. 추가할 위치의 '이전' 노드를 찾는다.
        # 더미 헤드부터 시작해서 index번 만큼 이동한다.
        prev = self.head
        for _ in range(index):
            prev = prev.next
        
        # 4. 연결고리 바꿔주기
        # 새 노드의 다음은 이전 노드의 다음을 가리킨다.
        new_node.next = prev.next
        # 이전 노드의 다음은 새 노드를 가리킨다.
        prev.next = new_node
        
        # 5. 리스트 크기를 1 증가시킨다.
        self.size += 1

    def deleteAtIndex(self, index: int) -> None:
        """
        index 위치의 노드를 삭제합니다.
        """
        # 1. 인덱스가 유효한 범위인지 확인
        if index < 0 or index >= self.size:
            return
            
        # 2. 삭제할 위치의 '이전' 노드를 찾는다.
        prev = self.head
        for _ in range(index):
            prev = prev.next
        
        # 3. 연결고리 건너뛰기
        # 이전 노드의 다음을, 삭제할 노드의 다음 노드로 바꿔준다.
        prev.next = prev.next.next
        
        # 4. 리스트 크기를 1 감소시킨다.
        self.size -= 1
```
