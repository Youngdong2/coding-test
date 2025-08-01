## [Intersection of Two Linked Lists]

### 1. 문제 요약
두 개의 단일 연결 리스트가 주어졌을 때, 두 리스트가 하나로 합쳐지는 교차점 노드를 찾는 문제

### 2. 초기 접근 및 풀이

#### 핵심 로직

두 연결리스트의 길이 차이를 이용해서 푸려고 했다.

#### 초기 코드
```python
class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
        lenA, lenB = 0, 0
        pA, pB = headA, headB
        
        while pA:
            lenA += 1
            pA = pA.next
            
        while pB:
            lenB += 1
            pB = pB.next
            
        if lenA > lenB:
            for _ in range(lenA-lenB):
                headA = headA.next
                
        else:
            for _ in range(lenB-lenA):
                headB = headB.next
                
        while headA != headB:
            headA = headA.next
            headB = headB.next
            
        return headA
```


### 3. 핵심 정리 및 주요 원칙

#### 핵심 정리
두 리스트의 길이를 각각 측정한 뒤, 더 긴 리스트의 포인터를 길이의 차이만큼 먼저 앞으로 이동시켜 '출발선'을 맞춘다.  
그 후, 두 포인터를 같은 속도로 한 칸씩 함께 전진시키면 교차점에서 정확히 만나게 되는 원리를 이용하는 것
