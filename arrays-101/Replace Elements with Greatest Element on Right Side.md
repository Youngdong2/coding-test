## Replace Elements with Greatest Element on Right Side

### 1. 문제 요약

배열의 각 원소를 그 원소의 오른쪽에 있는 모든 원소들 중 가장 큰 값으로 교체하는 문제

### 2. 초기 접근 및 풀이

#### 핵심 로직

- 반복문을 돌며 오른쪽의 최댓값으로 값을 대체하는 방법으로 풀었다.
- 하지만 시간초과가 떴다...

#### 초기 코드

```python
class Solution:
    def replaceElements(self, arr: List[int]) -> List[int]:
        n = len(arr)
        for i in range(1, n):
            arr[i-1] = max(arr[i:])
        arr[-1] = -1
        
        return arr
```

#### 복잡도 분석

- 시간 복잡도: $O(N^2)$
- 공간 복잡도: $O(N)$

### 3. 피드백 및 개선점

`max(arr[i:])` 이 부분이 중첩된 반복이 된다. 즉, 이중 반복문이다..

### 4. 최적화된 풀이

#### 개선된 로직

이 문제는 역방향 순회를 해야한다고 한다.

1. 오른쪽에서부터 지금까지 본 숫자 중 가장 큰 값을 계속 추적한다. 이 값을 `max_from_right`라고 하자.
2. 배열의 맨 마지막 원소부터 처음 원소까지 거꾸로 순회한다.
   - 현재 위치의 원소를 `max_from_right`값으로 교체한다.
   - 그 후 `max_from_right`값을 원래 있던 값과 기존 `max_from_right`중 더 큰 값으로 갱신한다.

#### 최종 코드

```python
class Solution:
    def replaceElements(self, arr: List[int]) -> List[int]:
        # 오른쪽부터 지금까지 본 최댓값을 저장할 변수
        # 초기값은 -1 (맨 마지막 원소는 항상 -1이 됨)
        max_from_right = -1
        
        # 배열을 뒤에서부터 앞으로 순회
        for i in range(len(arr) - 1, -1, -1):
            # 현재 위치의 원래 값을 임시 저장
            original_val = arr[i]
            
            # 현재 위치를 "오른쪽에서 본 최댓값"으로 교체
            arr[i] = max_from_right
            
            # "오른쪽에서 본 최댓값"을 갱신 (다음 루프를 위해)
            max_from_right = max(max_from_right, original_val)
            
        return arr
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(N)

### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리

배열을 뒤에서부터 거꾸로 순회하며, '오른쪽부터 지금까지 본 최댓값'을 계속 갱신하고 그 값으로 현재 위치를 덮어쓰는 것