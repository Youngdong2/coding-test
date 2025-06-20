## Merge Sorted Array

### 1. 문제 요약
정렬된 두 배열 nums1과 nums2를, nums1 배열 안에 하나의 정렬된 배열로 합치는 문제입니다. 이때, nums1은 이미 nums2를 모두 담을 수 있는 충분한 공간을 가지고 있다.

### 2. 초기 접근 및 풀이

#### 핵심 로직
진짜 단순히 뒷부분을 채운 뒤 정렬을 하였다.

#### 초기 코드
```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        nums1[m:] = nums2[:n]
        nums1.sort()

```

#### 복잡도 분석

- 시간 복잡도: O((m+n) log(m+n))
- 공간 복잡도:

### 3. 피드백 및 개선점
- 두 배열이 정렬되어있다는 걸 사용하지 않았다.
- 정렬 조건을 활용해 더 효율적으로 시간복잡도를 해결할 수 있어야한다...

### 4. 최적화된 풀이

#### 개선된 로직

- `nums1` 배열의 **뒤쪽부터** 채워나가야 한다. 앞에서부터 채우면 `nums1`의 원래 원소를 덮어쓰게 되므로, 뒤쪽 비어있는 공간부터 채우는 것이 핵심!
- 포인터 세 개를 준비한다.
    - `p1`: `nums1`의 유효한 원소들 중 마지막 인덱스
    - `p2`: `nums2`의 마지막 인덱스
    - `p`: 병합된 결과가 저장될 `nums1`의 가장 마지막 인덱스
- p2 포인터가 0보다 크거나 같을 동안 (즉, nums2에 아직 처리할 원소가 있는 동안) 아래를 반복.
    - p1이 아직 유효하고(p1 >= 0), nums1[p1]이 nums2[p2]보다 크다면, 더 큰 값인 nums1[p1]을 nums1[p]에 넣고, p1을 한 칸 앞으로 옮긴다.
    - 그렇지 않다면(즉, nums2[p2]가 더 크거나 같거나, p1이 이미 범위를 벗어났다면), nums2[p2]를 nums1[p]에 넣고, p2를 한 칸 앞으로 옮긴다.
    - 어떤 경우든 p 포인터는 한 칸 앞으로 옮긴다.

#### 최종 코드

```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        p1 = m-1
        p2 = n-1
        p = m+n-1
        
        while p2 >= 0:
            if p1 >= 0 and nums1[p1] > nums2[p2]:
                nums1[p] = nums1[p1]
                p1 -= 1
                
            else:
                nums1[p] = nums2[p2]
                p2 -= 1
                
            p -= 1
```

#### 복잡도 분석

- 시간 복잡도: O(m+n)
- 공간 복잡도:

### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리
 원본 데이터를 덮어쓰는 문제를 피하기 위해, 공간이 비어있는 배열의 뒤에서부터 두 배열의 값을 비교하며 채워 나가는 것

