## First Unique Character in a String

### 1. 문제 요약

주어진 문자열에서 반복되지 않고 한 번만 나타나는 첫 번째 문자의 인덱스를 찾는 문제

### 2. 초기 접근 및 풀이

#### 핵심 로직

딕셔너리를 만들고, 인덱스와 갯수를 모두 관리하려고 했다.

#### 초기 코드

```python
class Solution:
    def firstUniqChar(self, s: str) -> int:
        mapping = {}
        for i in range(len(s)):
            if s[i] not in mapping:
                mapping[s[i]] = [i, 1]
                
            else:
                mapping[s[i]][1] += 1
                
        for v in mapping.values():
            if v[1] == 1:
                return v[0]
            
        return -1
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(K)

### 3. 피드백 및 개선점

해시맵(딕셔너리)을 매우 영리하게 활용한 훌륭한 풀이입니다! 라고 재미나이가 말해줬다!


### 4. 핵심 정리 및 주요 원칙

#### 핵심 정리

 첫 번째 순회에서 해시맵(딕셔너리)에 각 문자의 '첫 등장 인덱스'와 '등장 횟수'를 모두 기록한 뒤, 두 번째 순회에서 이 기록을 바탕으로 등장 횟수가 1인 첫 번째 문자를 찾아 그 인덱스를 반환하는 것