## Logger Rate Limiter

### 1. 문제 요약

실시간으로 들어오는 메시지와 타임스탬프를 기반으로, 동일한 메시지는 10초 이내에 한 번만 출력되도록 허용 여부를 결정하는 로거 시스템을 디자인하는 문제

### 2. 초기 접근 및 풀이

#### 핵심 로직

- 딕셔너리를 만든 후, 메시지와 타임스탬프를 저장한다. 
- 이후 나타났던 메시지라면, 타임스탬프를 비교하며 리턴해준다.

#### 초기 코드
```python
class Logger:

    def __init__(self):
        self.mapping = {}
        
    def shouldPrintMessage(self, timestamp: int, message: str) -> bool:
        if message not in self.mapping:
            self.mapping[message] = timestamp
            return True
            
        last_timestamp = self.mapping[message]
        
        if timestamp - last_timestamp >= 10:
            self.mapping[message] = timestamp
            return True
        
        else:
            return False
```

#### 복잡도 분석

- 시간 복잡도: O(1)
- 공간 복잡도: O(N)

### 3. 피드백 및 개선점
- 완벽한 풀이!!

### 4. 핵심 정리 및 주요 원칙

#### 핵심 정리
해시맵(딕셔너리)을 '기록부'로 사용하여, 각 메시지가 '마지막으로 언제 출력되었는지' 그 시간을 기록하고, 새로운 메시지 요청이 올 때마다 현재 시간과 기록된 시간의 차이를 비교하여 10초 규칙을 통과하는지 판별하는 것