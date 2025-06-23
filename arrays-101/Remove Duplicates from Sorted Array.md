## Remove Duplicates from Sorted Array

### 1. 문제 요약
정렬된 배열에서 중복된 원소들을 제자리에서(in-place) 제거하여 유니크한 원소들만 순서대로 남기고, 그 결과로 만들어진 새로운 배열의 길이를 반환하는 문제

### 2. 초기 접근 및 풀이

#### 핵심 로직
여태까지 배웠던 투포인터를 활용해봤다. slow와 fast를 정의하고, slow는 유니크한 원소의 인덱스를 할당하고, fast로 각 값을 돌면서 같은지 다른지 판단했다.  
처음으로 투포인터를 활용해서 맞춘거라 기분 좋았지만, 마지막 slow+1 이 부분을 어떻게 처리해야할지 모르겠다.

#### 초기 코드
```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        n = len(nums)
        slow = 0
        fast = 0
        
        while fast < n:
            if nums[fast] != nums[slow]:
                slow += 1
                nums[slow] = nums[fast]
                
            fast += 1
            
        return slow+1
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(1)

### 3. 피드백 및 개선점
리턴할 때 slow + 1을 처리해야한다.

### 4. 최적화된 풀이

#### 개선된 로직

- k (또는 slow) 포인터: 유니크한 배열의 길이를 의미하며, 다음에 유니크한 값이 들어올 위치를 가리킨다. 1부터 시작. 첫번째 원소는 항상 고유한 값이기 때문이다.
- i (또는 fast) 포인터: 배열 전체를 탐색한다. 1부터 시작한다.
- 비교 대상: `nums[i]`와 바로 이전 값 `nums[i-1]`을 비교.

#### 최종 코드

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        if not nums:
            return 0
        
        # k는 유니크한 배열의 길이를 의미한다.
        # nums[0]은 항상 유니크하므로 k는 1에서 시작한다.
        k = 1
        
        # i는 1번 인덱스부터 배열 끝까지 탐색한다.
        for i in range(1, len(nums)):
            # 현재 값이 이전 값과 다르다면, 새로운 유니크한 값이다.
            if nums[i] != nums[i-1]:
                # 해당 값을 k 위치에 넣고, k를 1 증가시킨다.
                nums[k] = nums[i]
                k += 1
                
        return k
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(1)

### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리
정렬된 배열의 특성을 이용하여, 느린 포인터(k)를 유니크한 배열의 길이로 간주하고, 빠른 포인터(i)로 새로운 유니크한 값을 찾을 때마다 k의 위치에 값을 덮어쓰고 길이를 1 늘려주는 것