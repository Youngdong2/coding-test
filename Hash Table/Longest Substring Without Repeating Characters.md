## [Longest Substring Without Repeating Characters]

### 1. 문제 요약

주어진 문자열에서, 문자가 중복되지 않는 가장 긴 '연속된 부분 문자열'(substring)의 길이를 찾는 문제

### 2. 초기 접근 및 풀이

#### 핵심 로직

- 한 원소마다 집합을 만들어서 최대 길이를 비교했다.

#### 초기 코드
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        count = 0
        for i in range(len(s)):
            seen = set()
            for j in range(i, len(s)):
                if s[j] not in seen:
                    seen.add(s[j])
                    count = max(count, len(seen))
                else:
                    break
                    
        return count
```

#### 복잡도 분석

- 시간 복잡도: O(N²)
- 공간 복잡도: O(N)

### 3. 피드백 및 개선점

- 이 풀이는 이중 for문으로 복잡도가 O(N²)이다. 개선할 여지가 있다.

### 4. 최적화된 풀이

#### 개선된 로직

- 슬라이딩 윈도우 방식으로 풀 수 있다.
- 이중 루프 대신, 두개의 포인터를 사용해 배열을 단 한번만 훑는다.
- 핵심 아이디어:

right 포인터가 오른쪽으로 이동하며 '윈도우'를 확장합니다.

right가 가리키는 문자가 윈도우 안에 이미 있다면, 중복이므로 left 포인터를 오른쪽으로 이동시켜 윈도우를 축소합니다.

매 순간 윈도우의 크기를 확인하여 최댓값을 갱신합니다.

#### 최종 코드

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        # 윈도우 안에 있는 문자들을 저장할 set
        seen = set()
        # 윈도우의 왼쪽 경계
        left = 0
        max_length = 0
        
        # right 포인터가 문자열 끝까지 이동
        for right in range(len(s)):
            # 1. right 포인터가 가리키는 문자가 윈도우에 이미 있다면,
            #    중복이므로 윈도우를 축소해야 한다.
            while s[right] in seen:
                # 윈도우의 왼쪽 문자를 제거하고, left 포인터를 오른쪽으로 한 칸 이동
                seen.remove(s[left])
                left += 1
            
            # 2. 이제 중복이 없으므로, right 포인터의 문자를 윈도우에 추가
            seen.add(s[right])
            
            # 3. 현재 윈도우의 크기를 계산하여 최댓값을 갱신
            # 윈도우 크기 = right - left + 1
            max_length = max(max_length, right - left + 1)
            
        return max_length
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(N)

### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리
슬라이딩 윈도우' 기법을 사용하여, 두 개의 포인터(left, right)로 '창문'의 범위를 조절하고, 해시 셋을 이용해 창문 안의 문자 중복을 O(1)로 확인하는 것

