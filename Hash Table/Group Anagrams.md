## Group Anagrams

### 1. 문제 요약

주어진 문자열 배열에서, 철자의 구성은 같지만 순서만 다른 애너그램 관계의 단어들을 찾아 함께 묶어주는 문제

### 2. 초기 접근 및 풀이

#### 핵심 로직

- 딕셔너리를 만들고, 정렬된 문장으로 키값으로, 문자열의 리스트를 value값으로 지정했다.
- 주어진 배열을 순환하며 적절한 조건으로 확인하여 출력했다.

#### 초기 코드

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        mapping = {}
        for s in strs:
            if ''.join(sorted(s)) not in mapping:
                mapping[''.join(sorted(s))] = [s]
                
            else:
                mapping[''.join(sorted(s))].append(s)
                
        return [v for v in mapping.values()]
```

#### 복잡도 분석

- 시간 복잡도: O(N * K log K)
- 공간 복잡도: O(N * K)

### 3. 피드백 및 개선점

- 결론부터 말씀드리면, 이 코드는 문제를 해결하는 가장 이상적이고 정확한, 완벽한(Perfect) 정답입니다! 라고 재미나이가 말했다.
- 하지만 좀 더 코드스타일을 파이써닉하게 구현할 수 있다.

### 4. 최적화된 풀이

#### 개선된 로직

- 파이썬의 `collections.defaultdict`를 사용하면 `if/else` 확인 부분을 더욱 간결하게 만들 수 있다.
- 1defaultdict(list)1는 딕셔너리에 존재하지 않는 키를 조회할 때, 자동으로 빈 리스트([])를 생성해주는 매우 편리한 도구

#### 최종 코드

```python
from collections import defaultdict

class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        # 키가 없을 때 자동으로 빈 리스트를 생성하는 딕셔너리
        mapping = defaultdict(list)
        
        for s in strs:
            # 정렬된 문자열을 키로 사용하여, 원본 문자열을 리스트에 바로 추가
            sorted_key = ''.join(sorted(s))
            mapping[sorted_key].append(s)
            
        return list(mapping.values())
```

#### 복잡도 분석

- 시간 복잡도: O(N * K log K)
- 공간 복잡도: O(N * K)

### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리
애너그램 관계의 단어들은 '정렬했을 때 항상 같은 문자열이 된다'는 특징을 이용하여, 이 정렬된 문자열을 '대표 키'로 삼아 딕셔너리에 원본 단어들을 그룹핑하는 것

