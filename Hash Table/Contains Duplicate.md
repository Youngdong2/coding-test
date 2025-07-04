## Contains Duplicate

### 1. 문제 요약

주어진 정수 배열에 중복된 원소가 하나라도 있으면 True를, 모든 원소가 고유하다면 False를 반환하는 문제

### 2. 초기 접근 및 풀이

#### 핵심 로직

카운트를 세는 딕셔너리를 만든 뒤 카운트가 2 이상이면 true를 반환하게 했다.

#### 초기 코드

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        check_dict = {}
        for num in nums:
            if num not in check_dict:
                check_dict[num] = 1
                
            else:
                check_dict[num] += 1
                
        for k, v in check_dict.items():
            if v > 1:
                return True
            
        return False
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(N)

### 3. 피드백 및 개선점

- 해시맵 사용은 잘한점.
- 투 패스에서 원 패스로 최적화할 수 있다.

### 4. 최적화된 풀이

#### 개선된 로직

- 해시 셋을 이용해서 원 패스로 푼다.

#### 최종 코드

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        seen = set()
        for num in nums:
            if num in seen:
                return True
            
            seen.add(num)
            
        return False
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(N)

### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리

해시 셋(Hash Set) 자료구조를 이용하여, 배열을 한 번만 순회하면서 각 숫자의 등장 여부를 기록하고, 이미 기록된 숫자를 다시 만나는 즉시 중복으로 판별하는 것
