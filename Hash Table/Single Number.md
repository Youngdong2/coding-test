## Single Number

### 1. 문제 요약

정수 배열에서 다른 모든 원소는 두 번씩 나타나는데, 단 하나만 한 번 나타나는 그 유일한 원소를 찾는 문제

### 2. 초기 접근 및 풀이

#### 핵심 로직

Counter를 사용해서 개수가 1인것을 찾았다.

#### 초기 코드

```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        from collections import Counter
        
        count = Counter(nums)
        for k, v in count.items():
            if v == 1:
                return k
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(N)

### 3. 피드백 및 개선점

Counter를 만들기 위해 추가적인 메모리 공간이 필요하다. 개선점이 필요.

### 4. 최적화된 풀이

#### 개선된 로직

- XOR 비트 연산자(^)를 사용한다.
- 이를 활용하면 두 번씩 나오는 숫자들은 모두 자기 자신과 XOR되어 0으로 사라진다.
- 최종적으로는 한 번만 나오는 유일한 숫자와 0의 XOR 연산만 남게 되어, 그 유일한 숫자 자신이 결과로 남게 된다.

#### 최종 코드

```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        result = 0
        for num in nums:
            result ^= num

        return result
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(1)

### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리

배열의 모든 원소를 XOR 연산하면, 두 번씩 나오는 숫자들은 서로 상쇄되어 0이 되고, 결국 한 번만 나오는 유일한 숫자만 남게 되는 원리를 이용하는 것
