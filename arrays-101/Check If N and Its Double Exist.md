## [Check If N and Its Double Exist]

### 1. 문제 요약

주어진 정수 배열 arr에서, 한 원소(N)와 그 원소의 두 배가 되는 다른 원소(M, 즉 N = 2 * M)가 모두 존재하는지 확인하는 문제

### 2. 초기 접근 및 풀이

해시맵을 활용해 풀었다. 먼저 주어진 배열의 두배를 키값으로, 해당 인덱스를 value로 저장했다.  
그 후 다시 배열을 돌며 해당 값이 있는지 확인했다.


#### 초기 코드

```python
class Solution:
    def checkIfExist(self, arr: List[int]) -> bool:
        map_dict = {}
        for i in range(len(arr)):
            map_dict[2*arr[i]] = i
            
        for i in range(len(arr)):
            if arr[i] in map_dict.keys() and map_dict[arr[i]] != i:
                return True
            
        return False
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(N)

### 3. 피드백 및 개선점

현재 이중 for문은 아니지만 배열을 두번 반복해서 돈다. 이를 한번으로 줄일 수 있다.

### 4. 최적화된 풀이

#### 개선된 로직

배열을 순회하면서 값들을 기억하고, 그 값의 두배 또는 절반이 본 숫자들중에 있는지 확인한다.

#### 최종 코드

```python
class Solution:
    def checkIfExist(self, arr: List[int]) -> bool:
        seen = set() # 내가 지금까지 본 숫자들을 저장하는 공간
        
        for num in arr:
            # 현재 숫자의 두 배가 이미 seen에 있거나,
            # 현재 숫자의 절반이 이미 seen에 있는지 확인
            if (2 * num) in seen or (num % 2 == 0 and num / 2 in seen):
                return True
            
            # 확인이 끝났으면, 현재 숫자를 본 목록에 추가
            seen.add(num)
            
        return False
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(N)

### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리

기본적으로 접근방법은 비슷하지만 내가 고민했던 부분을 현재 값의 절반을 확인하는 방법으로 해결했다.