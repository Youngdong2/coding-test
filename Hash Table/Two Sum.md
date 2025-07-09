## Two Sum

### 1. 문제 요약

주어진 정수 배열에서 두 숫자를 더해 특정 목표 값(target)을 만들 수 있는, 그 두 숫자의 인덱스를 찾는 문제

### 2. 초기 접근 및 풀이

#### 핵심 로직

타겟과 값을 뺀 값이 맵에 있는지 확인하고 없으면 넣어주는 방식으로 풀었다.

#### 초기 코드

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        mapping = {}
        
        for i in range(len(nums)):
            temp = target - nums[i]
            if temp in mapping:
                return [mapping[temp], i]
                        
            else:
                mapping[nums[i]] = i
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(N)

### 3. 피드백 및 개선점

- 결론부터 말씀드리면, 이 코드는 Two Sum 문제를 푸는 가장 이상적이고 효율적인, 완벽한(Perfect) 정답입니다. 라고 재미나이가 말해줬다 ㅎㅎ


### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리

배열을 단 한 번만 순회하면서, 해시맵(딕셔너리)을 이용해 "현재 값의 짝꿍(target - 현재 값)이 이전에 등장했는지"를 O(1)의 빠른 속도로 확인하고, 없으면 현재 값과 위치를 기록하는 것

