## [Height Checker]

### 1. 문제 요약

학생들의 현재 키 순서가 주어졌을 때, 키 순서대로 올바르게 정렬했을 경우와 비교하여 현재 위치가 잘못된 학생의 수를 세는 문제

### 2. 초기 접근 및 풀이

#### 핵심 로직

투포인터로 풀어야하는지 고민을 많이하다가 너무 어려워서 그냥 단순하게 정렬된 새로운 리스트를 만들고, 값을 비교하는 방식으로 풀었는데 이게 최선의 풀이라니...

#### 초기 코드

```python
class Solution:
    def heightChecker(self, heights: List[int]) -> int:
        count = 0
        expected = sorted(heights)
        
        for i in range(len(heights)):
            if heights[i] != expected[i]:
                count += 1
                
        return count
```

#### 복잡도 분석

- 시간 복잡도: O(N log N)
- 공간 복잡도: O(N)

#### 핵심 정리

(이 문제를 통해 배운 핵심 교훈을 한 문장으로 정리합니다.)

#### 주요 원칙

"이상적인 상태(키 순서대로 정렬된 배열)"를 하나 만든 뒤, "현재 상태(원본 배열)"와 자리를 하나씩 비교하여 위치가 다른 학생의 수를 세는 것