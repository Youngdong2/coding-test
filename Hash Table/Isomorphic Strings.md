## Isomorphic Strings

### 1. 문제 요약

두 문자열 사이에 일관성 있고, 고유한 '일대일 문자 변환 규칙'이 존재하는지를 확인하는 문제


### 2. 최적화된 풀이

#### 개선된 로직

두 개의 딕셔너리를 만든다.

1. s를 t로 바꾸는 암호표
2. t를 s로 바꾸는 암호표

문자열을 처음부터 끝까지 한 글자씩 확인하면서, 이 두 암호표에 규칙이 깨지는 경우가 생기는지 확인한다.

#### 최종 코드

```python
class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        # s -> t, t -> s 두 개의 매핑 딕셔너리를 만든다.
        s_to_t_map = {}
        t_to_s_map = {}
        
        # 두 문자열을 동시에 한 글자씩 확인한다.
        for s_char, t_char in zip(s, t):
            # Case 1: s_char가 처음 나오는 경우
            if s_char not in s_to_t_map:
                # t_char가 이미 다른 문자와 매핑되었다면 규칙 위반
                if t_char in t_to_s_map:
                    return False
                # 새로운 규칙을 양쪽 딕셔너리에 추가
                s_to_t_map[s_char] = t_char
                t_to_s_map[t_char] = s_char
            
            # Case 2: s_char가 이전에 나온 경우
            else:
                # 기존 규칙과 일치하는지 확인
                if s_to_t_map[s_char] != t_char:
                    return False
        
        # 끝까지 아무 문제 없었으면 True 반환
        return True
```

#### 복잡도 분석

- 시간 복잡도: O(N)
- 공간 복잡도: O(N)

### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리

두 개의 딕셔너리를 이용해 s에서 t로의 매핑과 t에서 s로의 매핑, 즉 '양방향 관계'가 끝까지 일관되게 유지되는지를 한 번의 순회로 검사하는 것

#### 주요 원칙

1. 양방향 매핑 (Two-Way Mapping): s_to_t_map은 s의 한 문자가 t의 여러 문자로 매핑되는 것을 방지하고, t_to_s_map은 s의 여러 문자가 t의 한 문자로 매핑되는 것을 방지합니다. 이 두 장치를 통해 완벽한 '일대일 대응' 관계를 강제합니다.
2. 동시 순회 (Simultaneous Iteration): zip 함수를 사용하여 두 문자열을 동시에 한 글자씩 짝지어 효율적으로 순회하고 비교합니다.
3. 실시간 규칙 검사 (Real-time Rule Checking): 루프를 돌면서 각 문자 쌍에 대해, 새로운 매핑 규칙을 추가할 때나 기존 규칙을 확인할 때 충돌이 발생하는지 즉시 검사합니다. 문제가 발견되면 즉시 False를 반환하여 불필요한 연산을 중단합니다.