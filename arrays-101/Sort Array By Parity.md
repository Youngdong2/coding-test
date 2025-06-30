## Sort Array By Parity

### 1. 문제 요약

주어진 정수 배열에서 모든 짝수가 모든 홀수보다 앞에 오도록 재배열하는 문제

### 2. 초기 접근 및 풀이

#### 핵심 로직

- 역시 투포인터를 활용했다. 왼쪽과 오른쪽을 비교하면서 왼쪽이 홀수, 오른쪽이 짝수이면 자리를 바꾸는 방식으로 풀었다.

#### 초기 코드

```python
class Solution:
    def sortArrayByParity(self, nums: List[int]) -> List[int]:
        left = 0
        right = len(nums)-1
        
        while left < right:
            if nums[left] % 2 != 0:
                if nums[right] % 2 == 0:
                    nums[left], nums[right] = nums[right], nums[left]
                    left += 1
                    right -= 1
                    
                else:
                    right -= 1
            else:
                left += 1
                    
        return nums
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(1)

### 3. 피드백 및 개선점

- 제미나이 왈: 정확하고 효율적인 로직.
- 허허 쉽지않았지만 뿌듯하다. 이제 투포인터를 잘 활용하는 것 같다.

### 4. 최적화된 풀이

#### 개선된 로직

로직적으로 말고 코드를 좀 더 깔끔하게 짜볼 수 있을 것 같다.

#### 최종 코드

```python
class Solution:
    def sortArrayByParity(self, nums: List[int]) -> List[int]:
        left, right = 0, len(nums) - 1

        while left < right:
            # 1. left 포인터는 제자리에 있는 짝수를 건너뛴다.
            #    (즉, 잘못된 위치에 있는 홀수를 찾을 때까지 전진)
            while left < right and nums[left] % 2 == 0:
                left += 1

            # 2. right 포인터는 제자리에 있는 홀수를 건너뛴다.
            #    (즉, 잘못된 위치에 있는 짝수를 찾을 때까지 후진)
            while left < right and nums[right] % 2 == 1:
                right -= 1

            # 3. 이제 left는 홀수를, right는 짝수를 가리키므로 교환한다.
            #    (위의 두 while 루프 덕분에 left < right 조건이 여전히 유효하다면)
            if left < right:
                nums[left], nums[right] = nums[right], nums[left]
                left += 1
                right -= 1

        return nums
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(1)

### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리

왼쪽에서 찾은 '잘못된 위치의 홀수'와 오른쪽에서 찾은 '잘못된 위치의 짝수'를 서로 맞바꾸어(swap), 각자를 올바른 영역으로 보내는 것
