## Minimum Index Sum of Two Lists

### 1. 문제 요약

두 개의 문자열 리스트가 주어졌을 때, 두 리스트에 공통으로 존재하는 원소들 중에서 각 리스트에서의 인덱스 합이 가장 작은 원소(들)를 모두 찾는 문제

### 2. 초기 접근 및 풀이

#### 핵심 로직

- 합을 비교하면서 딕셔너리에 저장하고, 최소값들을 리턴하는 형식으로 풀었다.
- 하지만 이중 for문을 개선할 여지가 있다.

#### 초기 코드

```python
class Solution:
    def findRestaurant(self, list1: List[str], list2: List[str]) -> List[str]:
        score = 2001
        mapping = {}
        
        for i in range(len(list1)):
            for j in range(len(list2)):
                if list1[i] == list2[j]:
                    mapping[list1[i]] = i+j
                    score = min(score, i+j)
                    
        answer = [k for k, v in mapping.items() if v==score]
        
        return answer
```

#### 복잡도 분석

- 시간 복잡도: O(N * M)
- 공간 복잡도: O(min(N, M))

### 3. 피드백 및 개선점

- 이중 for문은 비효율적이다.

### 4. 최적화된 풀이

#### 개선된 로직

하나의 리스트를 딕셔너리로 만들어, 탐색 시간을 O(1)로 줄이는 것

1. 첫 번째 리스트(`list1`)를 순회하며, 각 레스토랑 이름과 인덱스를 딕셔너리에 저장
2. 두 번째 리스트(`list2`)를 순회하면서, 현재 레스토랑이 딕셔너리에 있는지 확인
3. 만약 있다면, 두 인덱스의 합을 계산하고, 이 합이 지금까지의 최솟값보다 작은지, 같은지, 큰지 비교하여 `answer` 리스트를 갱신

#### 최종 코드

```python
class Solution:
    def findRestaurant(self, list1: List[str], list2: List[str]) -> List[str]:
        map1 = {restaurant: i for i, restaurant in enumerate(list1)}

        min_sum = float('inf')
        answer = []

        for j , restaurant in enumerate(list2):
            if restaurant in map1:
                current_sum = j + map1[restaurant]

                if current_sum < min_sum:
                    min_sum = current_sum
                    answer = [restaurant]

                elif current_sum == min_sum:
                    answer.append(restaurant)

        return answer
```

#### 복잡도 분석

- 시간 복잡도: O(N+M)
- 공간 복잡도: O(min(N, M))

### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리

이중 for 루프 대신, 하나의 리스트를 {이름: 인덱스} 형태의 딕셔너리로 미리 변환하여, 다른 리스트를 한 번만 순회하면서 공통 원소를 O(1)의 빠른 속도로 찾아내고 실시간으로 인덱스 합의 최솟값을 갱신하는 것