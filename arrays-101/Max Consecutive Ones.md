## [Max Consecutive Ones]

### 1. 문제 요약
주어진 이진 배열(0과 1로만 이루어진 배열)에서, 연속적으로 나타나는 1의 최대 개수를 찾는 문제

### 2. 초기 접근 및 풀이

#### 핵심 로직
1이 계속 나오면 count를 증가시키고 0이 나오면 초기화 하면서 리스트에 저장하는 로직

#### 초기 코드
```python
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        answer = []
        count = 0
        for i in range(len(nums)):
            if nums[i] == 1:
                count += 1
            else:
                count = 0
                
            answer.append(count)
                
        return max(answer)
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(N)

### 3. 피드백 및 개선점
- answer.append(count)가 반복문의 매 단계마다 실행
- 만약 nums 리스트의 길이가 10만이라면, answer 리스트에도 10만 개의 숫자가 저장된다.   
- 이렇게 입력값의 크기에 비례해서 메모리 사용량이 늘어나는 것을 **공간 복잡도가 O(N)**이라고 한다.

### 4. 최적화된 풀이

#### 개선된 로직
우리는 모든 중간 count 값을 저장할 필요 없이, 지금까지 나왔던 count 값 중 가장 큰 값 하나만 기억하면 됨.

#### 최종 코드

```python
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        max_count = 0  # 지금까지의 최댓값을 저장할 변수
        count = 0      # 현재 연속된 1의 개수를 세는 변수

        for num in nums:  # for i in range(len(nums)) 보다 이 방법이 더 파이썬다움.
            if num == 1:
                count += 1
            else:
                # 1의 연속이 끊겼으므로 count를 0으로 리셋
                count = 0
            
            # 현재 count가 기록된 최댓값보다 크면, 최댓값을 갱신
            max_count = max(max_count, count)
            
        return max_count
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(1)

### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리
모든 중간 결과를 저장할 필요가 있는지 항상 의심하고, 최댓값 같은 결과는 변수 하나로 계속 갱신하는 방식으로 공간을 최적화할 수 있다
