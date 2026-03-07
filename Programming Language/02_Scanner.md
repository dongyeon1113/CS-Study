# 🔍 프로그래밍 언어 2주차: Scanner (Lexical Analysis)


## 1. Scanner의 역할 (Front End의 시작)
Scanner(Lexical Analyzer)는 소스 코드의 **캐릭터 스트림(Character Stream)** 을 의미 있는 단위인 **토큰(Token)** 으로 묶어주는 역할을 합니다.

* **입력**: 소스 코드 (문자 하나하나)
* **출력**: 토큰 리스트 (단어 + 품사 정보)
    * 예: `x = x + y;` → `<id, x>`, `<EQ, =>`, `<id, x>`, `<OP, +>`, `<id, y>`, `<SC, ;>`
* **기타**: 공백(White space) 제거, 주말 처리, 에러 보고.

## 2. 정규 표현식 (Regular Expressions, RE)
토큰의 패턴을 정의하는 도구입니다. 스캐너 생성기의 핵심 언어입니다.

* **기본 연산**:
    * **선택 (Alternation)**: `R | S` (R 또는 S)
    * **연접 (Concatenation)**: `RS` (R 다음에 S)
    * **폐쇄 (Closure)**: `R*` (R이 0번 이상 반복 / 클레이니 스타)
* **중요**: 모든 정규 표현식은 유한 오토마타(Finite Automata)로 변환될 수 있습니다.

## 3. 유한 오토마타 (Finite Automata, FA)
문자열을 인식하는 가상의 기계 모델입니다.

### 3.1 NFA (Nondeterministic Finite Automata)
* 한 상태에서 같은 문자로 여러 경로를 갈 수 있음.
* **$\epsilon$-transition(에어리어 이동)**: 입력 없이도 상태 이동 가능.
* 사람이 정규표현식에서 설계하기 쉬움.

### 3.2 DFA (Deterministic Finite Automata)
* 특정 상태에서 특정 문자에 대해 **오직 하나의 경로**만 존재.
* 컴퓨터가 실제로 실행하기에 적합함 (빠름).
* $\epsilon$ 이동이 없음.

## 4. 핵심 알고리즘 (이론의 꽃 🌸)
스캐너가 자동으로 만들어지는 과정입니다.

1.  **Thompson's Construction**: 정규 표현식을 **NFA**로 변환.
    
2.  **Subset Construction**: NFA를 **DFA**로 변환. (중요 개념: $\epsilon$-closure, Move)
    
3.  **DFA Minimization**: 중복되는 상태를 합쳐서 가장 작은 DFA로 최적화.

## 5. RE → NFA → DFA 요약
| 단계 | 도구 | 특징 |
| :--- | :--- | :--- |
| **정규표현식** | 패턴 정의 | 사람이 읽기 쉬움 (예: `[a-z]*`) |
| **NFA** | Thompson | 설계하기 자유롭지만 시뮬레이션이 복잡함 |
| **DFA** | Subset | 실행 속도가 매우 빠름 (현업 스캐너의 형태) |
