## Top K Frequent Elements

### 1. 문제 요약

주어진 정수 배열에서 가장 빈번하게 나타나는 원소를 빈도수 순으로 상위 k개까지 찾아 반환하는 문제

### 2. 초기 접근 및 풀이

#### 핵심 로직

- 정렬하는 방식밖에 떠오르지 않는다..

#### 초기 코드

```python
from collections import Counter

class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        count_map = Counter(nums)
        
        sorted_count = sorted([[k, v] for k, v in count_map.items()], key=lambda x: x[1], reverse=True)

        return [x[0] for x in sorted_count[:k]]
```

#### 복잡도 분석

- 시간 복잡도: O(N + M log M)
- 공간 복잡도: O(M)

### 3. 피드백 및 개선점

- 로직은 정확하다.
- 하지만 이는 전체를 정렬하는 방식. 더 효율적으로 상위 k개만 찾을 수 있는지 고민해야한다.

### 4. 최적화된 풀이

#### 개선된 로직

- heap을 사용하면 전체를 정렬하는 대신, 크기가 k인 힙을 유지하며 상위 k개만 효율적으로 추적할 수 있다.

#### 최종 코드

```python
import heapq
from collections import Counter

class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        # 1. 빈도수 계산 (동일)
        counts = Counter(nums)
        
        # 2. 빈도수를 기준으로 최소 힙(min-heap)을 만든다.
        # 파이썬의 heapq는 최소 힙이므로, (빈도수, 숫자) 튜플을 넣는다.
        heap = []
        for num, freq in counts.items():
            heapq.heappush(heap, (freq, num))
            # 힙의 크기가 k를 초과하면, 가장 작은 원소(빈도수가 가장 낮은)를 제거한다.
            if len(heap) > k:
                heapq.heappop(heap)
        
        # 3. 힙에 남아있는 k개의 원소에서 숫자만 추출한다.
        return [item[1] for item in heap]
```

#### 복잡도 분석

- 시간 복잡도: O(N log k)
- 공간 복잡도: O(M)

### 5. 핵심 정리 및 주요 원칙

#### 힙(Heap)이란?

- 힙은 **가장 크거나 가장 작은 값**을 항상 빠르게 찾아낼 수 있도록 특별하게 설계된 트리 모양의 자료구조
- 그래서 우선순위 큐를 구현할 때 주로 사용된다.

#### 힙의 두 가지 핵심 규칙

힙은 항상 두 가지 규칙을 만족해야 한다.

1. 모양 규칙: 완전 이진 트리
2. 값 규칙: 힙속성
    - 최소 힙: 부모 노드의 값은 항상 자식 노드의 값보다 작거나 같다. 이 규칙때문에 가장 작은 값은 항상 트리의 맨 꼭대기, 즉 루트 노드에 위치한다. (파이썬의 `heapq`모듈이 바로 최소 힙)
    - 최대 힙: 부모 노드의 값은 항상 자식 노드의 값보다 크거나 같다.

```text
      1      <-- 루트 (가장 작은 값)
     / \
    3   2    <-- 부모(1)는 자식(3, 2)보다 작다
   / \ / \
  6  5 4  8   <-- 부모(3)은 자식(6, 5)보다 작다
             <-- 부모(2)는 자식(4, 8)보다 작다

```

#### 힙은 언제 사용하나?

1. 가장 크거나 작은 값 N개 찾기 (Top K문제)

    - 동작 원리(최소 힙 기준)
        1. 크기가 k인 최소 힙을 유지한다.
        2. 새로운 데이터가 들어올 때, 힙의 가장 작은 값과 비교한다.
        3. 만약 새로운 데이터가 더 크다면, 힙의 루트를 제거하고 새로운 데이터를 추가한다.
        4. 이 과정을 반복하면, 힙에는 항상 상위 K개의 가장 큰 값들만 남게 된다.

2. 우선순위 큐

    - 데이터에 우선순위가 있어서, 항상 우선순위가 가장 높은 데이터를 먼저 처리해야 할 때 사용한다.

3. 힙 정렬

    - 힙을 이용하여 데이터를 정렬하는 알고리즘
  - 
