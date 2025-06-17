## [Squares of a Sorted Array]

### 1. 문제 요약
오름차순으로 정렬된 정수 배열이 주어졌을 때, 각 원소를 제곱한 후 그 결과를 다시 오름차순으로 정렬하여 반환하는 문제.

### 2. 초기 접근 및 풀이

#### 핵심 로직
리스트 컴프리핸션으로 각 원소의 제곱을 한 뒤 정렬을 해줬다.

#### 초기 코드
```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        square_nums = [num ** 2 for num in nums]
        
        return sorted(square_nums)
```

#### 복잡도 분석

- 시간 복잡도: O(NlogN)
- 공간 복잡도: O(N) or O(NlogN)

### 3. 피드백 및 개선점
- 이 문제의 핵심은 **입력 배열이 이미 정렬되어 있다**는 사실을 활용하는 것.
- 현재 풀이는 정렬 조건을 사용하지 않고, 제곱한 뒤 다시 정렬한다. 이로 인해 시간복잡도 측면에서 비효율적임.
- `sorted(...)` 부분이 전체 시간의 대부분을 차지하며, `O(NlogN)`이다.

### 4. 최적화된 풀이

#### 개선된 로직
- 핵심 아이디어는 제곱했을 때 가장 큰 값이 될 수 있는 후보는 원래 배열의 양쪽 끝에 있는 숫자들.
- 포인터 두개를 준비하고, left 포인터가 right 포인터를 넘기 전까지 반복.
    - nums[left]의 제곱과 nums[right]의 제곱 중 더 큰 값을 result[k]에 넣는다.
    - 만약 right 쪽의 값이 더 컸다면, right 포인터를 왼쪽으로 한 칸 옮긴다.
    - 만약 left 쪽의 값이 더 컸다면, left 포인터를 오른쪽으로 한 칸 옮긴다.

#### 최종 코드

```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        n = len(nums)
        result = [0] * n
        left = 0
        right = n - 1

        for i in range(n-1, -1, -1):
            if abs(nums[left]) < abs(nums[right]):
                result[i] = nums[right] ** 2
                right -= 1

            else:
                result[i] = nums[left] ** 2
                left += 1

        return result
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(N)

### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리
이 문제의 핵심은 **정렬된 배열의 제곱 값 중 가장 큰 수는 항상 배열의 양쪽 끝 값 중 하나에서 나온다**는 사실을 이용하여, 정렬을 다시 하지 않고 단 한 번의 순회(O(N))만으로 결과 배열을 만들어내는 것

#### 주요 원칙

1. 투 포인터(Two Pointers) 활용: 배열의 시작(left)과 끝(right)을 가리키는 두 개의 포인터를 사용해 탐색 범위를 관리
2. 역방향으로 결과 생성 (Build Backwards): 결과 배열의 가장 큰 값부터 거꾸로 채워 나간다. 이렇게 하면 어느 포인터의 값을 사용하든 결과 배열의 정해진 위치에 값을 한 번만 넣으면 되므로 매우 효율적이다.