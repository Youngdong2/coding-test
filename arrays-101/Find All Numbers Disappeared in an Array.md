## Find All Numbers Disappeared in an Array

### 1. 문제 요약

길이가 n인 배열이 주어질 때, 1부터 n까지의 숫자 중 그 배열에 나타나지 않는 모든 숫자를 찾는 문제

### 2. 초기 접근 및 풀이

#### 핵심 로직

1~n까지의 집합을 만든 뒤 주어진 배열의 집합과의 차집합을 구해 해결했다.

#### 초기 코드

```python
class Solution:
    def findDisappearedNumbers(self, nums: List[int]) -> List[int]:
        num_range = [i for i in range(1, len(nums)+1)]
        
        answer = list(set(num_range)-set(nums))
        
        return answer
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(N)

### 3. 피드백 및 개선점

- 직관적인 풀이
- 하지만 추가 공간을 사용하지 않고 O(N) 시간 복잡도로 풀진 않았다.
- 현재 풀이는 set을 만들기 위해 추가 공간을 사용하기 때문에 개선해야한다.

### 4. 최적화된 풀이

#### 개선된 로직

- 주어진 배열 자체를 해시 테이블처럼 활용하여 추가 공간 없이 문제를 해결하는 방법이 있다.
- 배열을 순회하며, 숫자 num을 발견하면 그 숫자에 해당하는 인덱스의 값을 음수로 만든다.
- 모든 순회가 끝난 후, 배열을 다시 한번 훑으면서 값이 여전히 양수인 인덱스를 찾는다. 그 인덱스에 해당하는 숫자가 사라진 숫자.

#### 최종 코드

```python
class Solution:
    def findDisappearedNumbers(self, nums: List[int]) -> List[int]:
        # 1. 방문 표시하기
        for num in nums:
            index = abs(num) - 1 # 이미 음수로 바뀌었을 수 있으므로 절댓값 사용
            if nums[index] > 0:
                nums[index] *= -1

        # 2. 방문하지 않은 숫자 찾기
        result = []
        for i in range(len(nums)):
            if nums[i] > 0:
                result.append(i + 1)

        return result
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(1)

### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리

추가 공간 없이, 주어진 배열 자체를 해시맵처럼 활용하여 문제를 해결하는 것

#### 주요 원칙

1. 제자리 수정 (In-place Modification): 새로운 자료구조를 만들지 않고 입력 배열을 직접 수정해서 정보를 저장한다. 이게 공간 복잡도를 O(1)로 최적화하는 핵심 기법이다.
2. 인덱스를 해시 키로 활용: 배열 값 num을 인덱스 num - 1로 쓰는 아이디어다. nums[num - 1]이 숫자 num의 존재 여부를 기록하는 공간이 된다.
3. 부호(Sign)를 방문 플래그로 사용: 숫자 부호를 양수에서 음수로 바꿔서 해당 숫자가 배열에 있다는 걸 '체크' 또는 '방문 표시'한다.
4. 절댓값(abs()) 사용: 배열을 순회할 때, 이미 다른 숫자에 의해 음수로 바뀌었을 수도 있으니 인덱스로 쓸 땐 꼭 abs(num)으로 원래 값을 써야 한다.
5. 투 패스(Two-Pass) 접근법: 첫 번째 순회에서 '방문 표시'를 다 남기고, 두 번째 순회에서 표시 안 된(아직 양수인) 위치를 찾아 결과를 수집하는 2단계로 문제를 푼다.