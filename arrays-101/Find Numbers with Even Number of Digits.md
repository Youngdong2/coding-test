## [Find Numbers with Even Number of Digits]

### 1. 문제 요약
주어진 숫자의 자리수가 짝수인 숫자를 찾는 문제.

### 2. 초기 접근 및 풀이

#### 핵심 로직
숫자를 문자열로 바꾼 뒤 길이가 짝수인 것의 개수를 확인.

#### 초기 코드
```python
class Solution:
    def findNumbers(self, nums: List[int]) -> int:
        answer = 0
        for num in nums:
            if len(str(num))%2==0:
                answer += 1
                
        return answer
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(1)

### 3. 피드백 및 개선점
- Pythonic한 코드.
- 학습을 위한 다른 관점을 제시하자면, '문자열 변환' 없이 순수 '수학 연산'만으로 자릿수를 구하는 방법도 생각해 볼 수 있다.

### 4. 다른 풀이

#### 다른 로직
숫자를 10으로 나눠가며 카운트를 한다.

#### 최종 코드

```python
class Solution:
    def findNumbers(self, nums: List[int]) -> int:
        answer = 0
        for num in nums:
            if num == 0:
                continue

            digit_count = 0
            while num > 0:
                num //= 10
                digit_count += 1

            if digit_count % 2 == 0:
                answer += 1

        return answer
```

#### 복잡도 분석

- 시간 복잡도: O(N * D)
- 공간 복잡도: O(1)

### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리
이 풀이의 핵심은 문자열 변환 없이, 10으로 반복해서 나누는 수학적 연산만으로 숫자의 자릿수를 알아낼 수 있다는 점.

#### 주요 원칙
 **"숫자를 직접 다룰 때는 몫(//)과 나머지(%) 연산을 활용하여 각 자릿수를 분리하고 처리할 수 있다"**는 점. 이는 정수와 관련된 다양한 문제를 푸는 데 있어 기본적인 테크닉