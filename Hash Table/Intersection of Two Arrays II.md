## Intersection of Two Arrays II

### 1. 문제 요약

두 개의 정수 배열이 주어졌을 때, 두 배열의 교집합을 구하는 문제입니다. 이때, 결과 배열의 각 원소는 두 배열에 공통으로 나타나는 횟수만큼, 즉 더 적은 횟수만큼 포함되어야 합니다.

### 2. 초기 접근 및 풀이

#### 핵심 로직

- 길이가 긴 배열을 기준으로 Counter 맵을 만든다.
- 작은 배열을 돌면서 공통 원소를 찾고, 찾으면 count를 줄이는 방식으로 풀었다.

#### 초기 코드

```python
from collections import Counter

class Solution:
    def intersect(self, nums1: List[int], nums2: List[int]) -> List[int]:
        answer = []
        if len(nums1) >= len(nums2):
            nums1, nums2 = nums1, nums2
        else:
            nums1, nums2 = nums2, nums1
            
        nums1_map = Counter(nums1)
        
        for num in nums2:
            if num in nums1_map and nums1_map[num]!=0:
                answer.append(num)
                nums1_map[num] -= 1
                
        return answer
```

#### 복잡도 분석

- 시간 복잡도: O(N + M)
- 공간 복잡도: O(max(N, M))

### 3. 피드백 및 개선점

- 로직적으로 좋은 풀이지만, 지금 코드에서는 더 긴 리스트로 카운터맵을 만들고 더 짧은 리스트로 순회하는데 이러면 공간 복잡도 측면에서 손해를 본다고 한다. 카운터 맵은 리스트 길이에 비례하는 메모리를 사용하기 때문.

### 4. 최적화된 풀이

#### 개선된 로직

- 짧은 리스트 기준으로 Counter를 만든다.

#### 최종 코드

```python
from collections import Counter

class Solution:
    def intersect(self, nums1: List[int], nums2: List[int]) -> List[int]:
        # 더 짧은 리스트를 기준으로 Counter를 만든다. (메모리 최적화)
        if len(nums1) > len(nums2):
            nums1, nums2 = nums2, nums1
        
        counts = Counter(nums1)
        answer = []
        
        # 더 긴 리스트를 순회한다.
        for num in nums2:
            if counts[num] > 0: # 0보다 큰지 확인하는 것이 더 간결함
                answer.append(num)
                counts[num] -= 1
                
        return answer
```

#### 복잡도 분석

- 시간 복잡도: O(N + M)
- 공간 복잡도: O(min(N, M))

### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리

하나의 배열을 해시맵(Counter)으로 변환하여 각 숫자의 등장 '횟수'를 기록한 뒤, 다른 배열을 순회하면서 공통된 숫자를 발견할 때마다 결과에 추가하고 기록된 횟수를 1씩 차감하는 것