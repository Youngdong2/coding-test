## Intersection of Two Arrays

### 1. 문제 요약

두 개의 정수 배열이 주어졌을 때, 두 배열에 공통으로 존재하는 원소들로 이루어진 교집합 배열을 찾는 문제

### 2. 초기 접근 및 풀이

#### 핵심 로직

두 배열을 집합으로 변환 후, 비교해야하는 원소가 집합에 있다면 저장하는 식으로 접근했다.

#### 초기 코드

```python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        answer = []
        set1 = set(nums1)
        set2 = set(nums2)
        for num in list(set2):
            if num in set1:
                answer.append(num)
                
        return answer
```

#### 복잡도 분석

- 시간 복잡도: O(N+M)
- 공간 복잡도: O(N+M)

### 3. 피드백 및 개선점

- 명확한 풀이.
- 하지만 좀 더 파이써닉하게 풀수도 있다.

### 4. 최적화된 풀이

#### 개선된 로직

& 연산자로 교집합을 구할 수 있다.

#### 최종 코드

```python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        set1 = set(nums1)
        set2 = set(nums2)
        
        # '&' 연산자로 두 set의 교집합을 구하고, list로 변환하여 반환
        return list(set1 & set2)
```

#### 복잡도 분석

- 시간 복잡도: O(N+M)
- 공간 복잡도: O(N+M)

### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리

두 배열을 각각 set으로 변환한 뒤, set의 교집합(&) 연산을 통해 두 배열에 공통으로 존재하는 고유한 원소들을 한 번에 찾아내는 것