## [Third Maximum Number]

### 1. 문제 요약

주어진 정수 배열에서 세 번째로 큰 '고유한(distinct)' 수를 찾는 문제

### 2. 초기 접근 및 풀이

#### 핵심 로직

중복된 숫자들을 제거 후 정렬해 세번째 큰 수를 찾는다.

#### 초기 코드

```python
class Solution:
    def thirdMax(self, nums: List[int]) -> int:
        sorted_nums = sorted(list(set(nums)), reverse=True)
        
        if len(sorted_nums) > 2:
            return sorted_nums[2]
        else:
            return sorted_nums[0]
```

#### 복잡도 분석

- 시간 복잡도: O(N log N)
- 공간 복잡도: O(N)

### 3. 피드백 및 개선점

- 직관적인 풀이.
- 정렬을 사용하기 때문에, 시간 복잡도 측면에서 비효율이 있다. 코테에서 정렬을 사용하지 않고 O(N) 복잡도로 해결할 수 있는가? 를 질문할 수 있다.

### 4. 최적화된 풀이

#### 개선된 로직

- 첫 번째, 두 번째, 세 번째 최댓값을 저장할 면수 세 개를 만든다.
- 배열을 순회하면서, 현재 숫자가 이 세 변수보다 큰지 확인하고, 크다면 적절히 값을 업데이트한다.

#### 최종 코드

```python
import float

class Solution:
    def thirdMax(self, nums: List[int]) -> int:
        first = -float('inf')
        second = -float('inf')
        third = -float('inf')

        for num in nums:
            # 중복된 값은 패스
            if num == first or num == second or num == third:
                continue

            if num > first:
                third = second
                second = first
                first = num

            elif num > second:
                third = second
                second = num

            elif num ? third:
                third = num

        # third가 여전히 초기값이라면 세 번째 최댓값이 없는 경우이다.
        return third if third != -float('inf') else first
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(1)

### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리

정렬을 사용하지 않고, 배열을 단 한 번만 순회하면서 first, second, third라는 세 개의 변수만을 이용해 가장 큰 세 개의 고유한 값을 실시간으로 추적하고 갱신하는 것

#### 주요 원칙

1. 원 패스 선형 탐색 (One-Pass Linear Scan): sorted() 함수 안 쓰고 for 루프 한 번만 돌려서 문제를 해결하고, 시간 복잡도를 O(N)으로 맞춘다.
2. 상수 공간으로 최댓값 추적: 추가 자료구조 없이 변수 세 개만 써서 상태를 관리하고, 공간 복잡도는 O(1)로 유지한다.
3. 계층적 업데이트 (Hierarchical Update): 새로운 최댓값을 찾으면 기존 first는 second로, second는 third로 한 단계씩 내려서 순위를 정확히 유지한다.
4. 중복 값 건너뛰기: 현재 값이 이미 first, second, third 중 하나와 같으면 비교를 건너뛰고, 고유한 값만 다룬다.
5. 초기값과 예외 처리: 변수들을 아주 작은 값(-float('inf'))으로 초기화해서 어떤 숫자와도 비교할 수 있게 한다. 마지막에 third 변수가 초기값 그대로면 "세 번째 최댓값이 없는 경우"를 처리한다.