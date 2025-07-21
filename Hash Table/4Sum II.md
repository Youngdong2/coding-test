## [4Sum II]

### 1. 문제 요약

네 개의 정수 배열이 주어졌을 때, 각 배열에서 원소를 하나씩 뽑아 더한 합이 0이 되는 조합(튜플)의 총 개수를 찾는 문제

### 2. 초기 접근 및 풀이

#### 핵심 로직

- 두개의 어레이끼리 각각 판단하려고 했다.
- 먼저 앞의 두 어레이의 합의 count를 딕셔너리로 만든다.
- 뒤의 두 어레이의 합이 딕셔너리에 있다면 count를 세준다.

#### 초기 코드

```python
class Solution:
    def fourSumCount(self, nums1: List[int], nums2: List[int], nums3: List[int], nums4: List[int]) -> int:
        sum1_map = {}
        for n1 in nums1:
            for n2 in nums2:
                if n1+n2 not in sum1_map:
                    sum1_map[n1+n2] = 1
                else:
                    sum1_map[n1+n2] += 1
                    
        count = 0
        for n3 in nums3:
            for n4 in nums4:
                if -(n3+n4) in sum1_map:
                    count += sum1_map[-(n3+n4)]
                    
        return count
```

#### 복잡도 분석

- 시간 복잡도: O(N²)
- 공간 복잡도: O(N²)

### 3. 피드백 및 개선점

- 아주 잘 푼 풀이!!

### 4. 핵심 정리 및 주요 원칙

#### 핵심 정리

 네 개의 배열을 두 개씩 짝지어, 한 쌍(nums1, nums2)의 모든 합계와 그 빈도수를 해시맵에 미리 기록한 뒤, 다른 한 쌍(nums3, nums4)의 합계에 대한 '짝꿍' 합계(-(n3+n4))를 해시맵에서 찾아 그 빈도수를 정답에 더해나가는 것