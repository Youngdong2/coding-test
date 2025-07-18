## Jewels and Stones

### 1. 문제 요약

주어진 jewels(보석 종류) 문자열에 포함된 문자가, 내가 가진 stones(돌) 문자열에 총 몇 개나 들어있는지 개수를 세는 문제

### 2. 초기 접근 및 풀이

#### 핵심 로직

- 보석에 있는 원소들을 집합으로 만들고, 돌들중에 집합에 있으면 카운트 세는 방식으로 풀었다. 너무 쉽다.

#### 초기 코드
```python
class Solution:
    def numJewelsInStones(self, jewels: str, stones: str) -> int:
        jewel_set = set(jewels)
        count = 0
        for stone in stones:
            if stone in jewel_set:
                count += 1
                
        return count
```

#### 복잡도 분석

- 시간 복잡도: O(J + S)
- 공간 복잡도: O(J)

### 3. 피드백 및 개선점

결론부터 말씀드리면, 이 코드는 문제를 해결하는 가장 이상적이고 효율적인, 완벽한(Perfect) 정답입니다! 라고 재미나이가 말했다.

### 4. 핵심 정리 및 주요 원칙

#### 핵심 정리

jewels 문자열을 해시 셋(Hash Set)으로 미리 변환하여 '보석 목록'을 만든 뒤, stones 문자열을 한 번만 순회하면서 각 돌이 보석 목록에 있는지 O(1)의 빠른 속도로 확인하여 개수를 세는 것