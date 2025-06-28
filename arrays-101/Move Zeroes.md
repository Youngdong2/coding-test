## Move Zeroes

### 1. 문제 요약

0이 아닌 원소들의 상대적인 순서는 유지하면서 모든 0을 배열의 끝으로 옮기는 문제

### 2. 초기 접근 및 풀이

#### 핵심 로직

- 투포인터를 활용
- 0이 아닌값들을 찾으며 인덱스마다 채워 넣어주고 끝에는 0을 채우는 방식으로 풀었다.

#### 초기 코드

```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        slow = 0
        for num in nums:
            if num != 0:
                nums[slow] = num
                slow += 1
                
        while slow < len(nums):
            nums[slow] = 0
            slow += 1
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(1)

### 3. 피드백 및 개선점

- 음.. 지피티에 물어보니까 완벽한 풀이라고 했다. 허허
- 다른 풀이 없냐고 물어보니까 스왑 기반 원 패스 방식도 제안해줬다.

### 4. 최적화된 풀이

#### 개선된 로직

1. `slow` 포인터를 0에 둔다. 이 포인터는 다음에 0이 아닌 숫자와 와야 할 위치를 가리킨다.
2. `fast` 포인터로 배열 전체를 순회한다.
3. 만약 `fast` 포인터가 0이 아닌 숫자를 발견하면, 그 숫자를 `slow` 포인터가 가리키는 위치의 값과 **교환**한다.
4. 교환이 일어났다면, `slow` 포인터를 다음 칸으로 한 칸 이동시킨다.

#### 최종 코드

```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        slow = 0
        for fast in range(len(nums)):
            # 0이 아닌 숫자를 찾으면
            if nums[fast] != 0:
                # slow 위치의 값과 교환한다.
                # (만약 slow와 fast가 같은 위치면 자기 자신과 교환하므로 안전하다)
                nums[slow], nums[fast] = nums[fast], nums[slow]
                # 다음 0이 아닌 숫자가 들어갈 위치를 한 칸 옮긴다.
                slow += 1
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(1)

### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리

이 풀이의 핵심은 투 포인터를 사용하여, '빠른 포인터'가 0이 아닌 값을 찾을 때마다 '느린 포인터'가 가리키는 앞쪽의 0과 자리를 맞바꾸는(swap) 것