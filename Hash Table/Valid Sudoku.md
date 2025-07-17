## Valid Sudoku

### 1. 문제 요약

주어진 9x9 스도쿠 보드가 현재 상태에서 유효한지를 판별하는 문제

### 2. 초기 접근 및 풀이

#### 핵심 로직

- 행, 열, 박스에 대한 set을 만드는데 각 인덱스에 대해 모두 만든다.
- 예를 들면 rows = [set(), set(), ..., set()] 이렇게.
- 각 원소를 돌면서 중복이면 false를 리턴하게 만든다.
- 박스에 대한 확인은 재미나이 도움을 받았다.

#### 초기 코드
```python
from collections import defaultdict

class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        rows = defaultdict(set)
        cols = defaultdict(set)
        boxes = defaultdict(set)
        
        for r in range(9):
            for c in range(9):
                num = board[r][c]
                
                if num == ".":
                    continue
                    
                box_id = (r//3, c//3)
                
                if num in rows[r]:
                    return False
                if num in cols[c]:
                    return False
                if num in boxes[box_id]:
                    return False
                
                rows[r].add(num)
                cols[c].add(num)
                boxes[box_id].add(num)
                
        return True
```

#### 복잡도 분석

- 시간 복잡도:
- 공간 복잡도:

#### 복잡도 분석

- 시간 복잡도: O(1)
- 공간 복잡도: O(1)

### 5. 핵심 정리 및 주요 원칙

#### 핵심 정리
9x9 보드를 단 한 번만 순회하면서, 현재 위치의 숫자가 자신이 속한 '행', '열', '3x3 박스' 각각의 규칙에 위배되는지 동시에 확인하는 것

#### 주요 원칙

1. 세 개의 기록부 활용: rows, cols, boxes라는 세 종류의 해시맵(또는 set의 배열)을 사용하여, 각 행, 열, 박스별로 등장한 숫자들을 실시간으로 기록하고 중복을 확인합니다.
2. 원 패스(One-Pass) 접근법: 행, 열, 박스를 따로따로 검사하는 대신, 하나의 이중 for 루프로 보드 전체를 훑으며 모든 규칙을 한 번에 검사하여 코드를 효율적이고 구조적으로 만듭니다.
3. 박스 ID 계산: (r, c) 위치가 어떤 3x3 박스에 속하는지를 알아내는 것이 중요합니다. box_id = (r // 3, c // 3) 라는 간단한 수식을 통해 9개의 셀을 하나의 고유한 박스 ID로 매핑하여 효율적으로 관리합니다.