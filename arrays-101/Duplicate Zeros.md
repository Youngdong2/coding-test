## Duplicate Zeros

### 1. 문제 요약
고정 길이의 정수 배열 arr이 주어졌을 때, 0이 나타나는 각 요소를 중복으로 복사하고, 남은 요소를 오른쪽으로 이동시켜야 하는 문제. 

### 2. 초기 접근 및 풀이

#### 핵심 로직
인덱스를 조정하여 0이 출현한 뒤 쪽 배열을 뒤로 밀어버리려고 했다.

#### 초기 코드
```python
class Solution:
    def duplicateZeros(self, arr: List[int]) -> None:
        """
        Do not return anything, modify arr in-place instead.
        """
        n = len(arr)
        i = 0
        while i < n-1:
            if arr[i] == 0:
                arr[i+1:] = [0] + arr[i+1:-1]
                i += 2
            else:
                i += 1
```

#### 복잡도 분석

- 시간 복잡도: $O(N^2)$
- 공간 복잡도: $O(N)$

### 3. 피드백 및 개선점
`arr[i+1:] = [0] + arr[i+1:-1]` 이 부분은 내부적으로 매우 비싼 연산을 수행한다.

1. 새로운 리스트 생성: `arr[i+1:-1]는 새로운 리스트를 만든다.
2. 리스트 연결: `[0] + ...`는 두 리스트를 합쳐 또 다른 새로운 리스트를 만든다.
3. 데이터 복사: 만들어진 새 리스트의 모든 내용을 기존 `arr`의 위치에 하나씩 복사한다.

이 과정은 배열의 뒷부분을 통째로 복사하는 것과 같아서, 한 번 실행될 때마다 배열 길이에 비례하는 시간이 걸린다.  
0이 나올 때마다 이 연산을 반복하므로, 최악의 경우 전체 시간 복잡도는 $O(N^2)$이 된다.

### 4. 최적화된 풀이

#### 개선된 로직

이런 종류의 "제자리 수정"문제는 보통 **뒤에서부터 데이터를 채워 넣는 방식**으로 `O(N)`이 해결할 수 있다고 한다.  
앞에서부터 수정하면 뒤에 있는 원본 데이터가 덮어씌워지기 때문이다.

#### 핵심 아이디어:

1. 첫번째 순회: 0을 복제했을 때, 배열의 맨 마지막에 위치할 원본 숫자가 무엇인지 찾아낸다. 즉, 최종적으로 잘려나가지 않고 
배열에 남게 될 원소들의 개수를 센다.
2. 두번째 순회(역방향): 위에서 찾은 마지막 원소부터 시작하여 배열의 뒤에서부터 앞으로 거슬러 올라오면서, 원본 배열의 값을 올바른 새 위치로 복사한다.
    - 0이 아니면 한 번만 복사
    - 0이면 두 번 복사

#### 최종 코드

```python
class Solution:
    def duplicateZeros(self, arr: List[int]) -> None:
        """
        Do not return anything, modify arr in-place instead.
        """
        n = len(arr)
        zeros_to_duplicate = 0

        # pass 1: 복제할 0의 개수를 세고, 마지막에 남을 원소의 경계를 찾는다.
        for i in range(n):
            if i + zeros_to_duplicate >= n:
                break
            if arr[i] == 0:
                # 마지막 자리에 0이 들어갈 경우, 복제는 불가능하고 덮어쓰기만 한다.
                if i + zeros_to_duplicate == n-1:
                    arr[n-1] = 0
                    n -= 1 # 실제 복사할 배열의 길이를 하나 줄여준다.
                    break
                zeros_to_duplicate += 1

        # pass 2: 뒤에서부터 앞으로 오면서 실제 값을 복사한다.
        # last_original_idx: 최종 배열에 남을 원본 배열의 마지막 인덱스
        last_original_idx = n - zeros_to_duplicate - 1

        for i in range(last_original_idx, -1, -1):
            # i: 원본 인덱스, i + zeros_to_duplicate: 복사될 위치의 인덱스
            if arr[i] == 0:
                arr[i + zeros_to_duplicate] = 0
                zeros_to_duplicate -= 1
                arr[i + zeros_to_duplicate] = 0
            else:
                arr[i + zeros_to_duplicate] = arr[i]
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(1)

### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리
앞에서부터 값을 변경하면 뒤에 있는 원본 데이터가 덮어씌워지는 문제를, 먼저 최종 상태를 계획하고 뒤에서부터 값을 채워나가는 방식으로 안전하게 해결하는 것.

#### 주요 원칙

1. 투 패스 접근법 (Two-Pass Approach): 문제를 한 번에 해결하려 하지 않고, 두 단계로 나눈다.
2. 역방향 수정 (Modify in Reverse): 배열을 제자리에서 수정할 때, 요소들이 뒤로 밀려나야 하는 경우 뒤에서부터 앞으로 값을 복사해야 한다. 이렇게 하면 아직 처리하지 않은 원본 데이터를 덮어쓰는 위험을 피할 수 있다.