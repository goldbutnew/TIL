# 기초 문법 1

2023-07-17

### 프로그래밍
- 프로그래밍: 새 연산을 정의하고 조합해 유용한 작업을 수행하는 것 → 문제를 해결하는 방법
- 프로그래밍 언어: 컴퓨터에게 작업을 지시하고 문제를 해결하는 도구 → 컴퓨터와 소통하는 방법
    
### 파이썬
- 파이썬 소개
    - [jetbrains survey: The State of Developer Ecosystem 2022](https://www.jetbrains.com/ko-kr/lp/devecosystem-2022/)
- 파이썬 실행
    - 컴퓨터는 기계어로 소통하기 때문에 사람이 기계어를 작성하기 어려움
    - 인터프리터가 사용자의 명령어를 운영체제가 이해하는 언어로 바꿈
    - 파이썬 프로그램 ↔ 인터프리터 ↔ 운영체제
        - 훨씬 더 사용하기 쉽고 운영체제간 이식도 가능 (확장성)
    - 파이썬 인터프리터를 사용하는 2가지 방법:
        - shell: CUI → `$ python -i` (나가는 법: 1. ctrl+c 연타, 또는 `exit()`)
        - 확장자.py
        - 상대경로와 절대경로의 결과가 다를 때가 있음
- 표현식과 값
    - 표현식: 값, 변수, 연산자 등을 조합하여 계산되고 결과를 내는 코드 구조 (ex. 1+2)
        - 1+2 → 표현식(expression)
        - a=3 → 할당해(statement)
        - 표현식이 중요한 이유? 표현식이 들어가는 자리가 있음. 예를 들어 if문 뒤에는 표현식이 들어옴.
    - 표현식이 **평가(evaluate)**되어 값이 반환됨
    - 평가: 표현식이나 문장을 실행하여 그 결과를 계산하고 값을 결정하는 과정 → 표현식이나 문장을 순차적으로 평가하여 프로그램의 동작을 결정
    - 문장(statement): 실행 가능한 동작을 기술하는 코드
    - 표현식<문장 → 문장은 보통 여러 개의 표현식을 포함
        
        ![img1](https://github.com/goldbutnew/data-marketing-idea-challenge/assets/149566915/1d62adf1-4167-4ce2-be10-335e4958b058)
- 타입
    - 타입: 값이 어떤 종류의 데이터인지, 어떻게 해석되고 처리되어야 하는지를 정의
        
        ![img2](https://github.com/goldbutnew/data-marketing-idea-challenge/assets/149566915/3a5e2ec4-bc79-48ac-a6c9-8d24a4adab7c)
        
    - 값(피연산자)
    - 연산자: 값에 적용할 수 있는 연산
    - 데이터 타입
        
        > Numeric Type: int(정수), float(실수), complex(복소수)
        > 
        > 
        > Seqeunce Types: list, tuple, range
        > 
        > Text Sequence Type: str(문자열)
        > 
        > Set Types: set(집합)
        > 
        > Mapping Types: dict(딕셔너리)
        > 
        > 기타: None(값이 없음을 규정하는 타입), Boolean(T/F), Functions
        > 
    - 산술 연산자
        
        ![img3-1](https://github.com/goldbutnew/data-marketing-idea-challenge/assets/149566915/20455984-791c-4b33-9b06-edc0c8c1a2df)
        
    - 연산자 우선순위
        
        ![img3-2](https://github.com/goldbutnew/data-marketing-idea-challenge/assets/149566915/daf59254-e858-4be9-b44b-6ba6a9c30e60)
        
    - -2**4=-16 / -(2**4)=-16 / (-2)**4=16
- 변수와 메모리
    
    ![img4](https://github.com/goldbutnew/data-marketing-idea-challenge/assets/149566915/835e302a-b453-40b8-973b-f2f27fecbc32)
    
    - 변수(Variable)
        - 값을 참조(내가 어떠한 값을 바라보고 있다)하는 이름
    - **degrees = 36.5**: “변수 degrees에 값 36.5를 할당했다.
    - 변수명 규칙
        - 영문 알파벳, 언더스코어(_), 숫자로 구성
        - 숫자로 시작할 수 없음
        - **대소문자**를 구분 (ex. True와 true)
        - 파이썬 내부 예약어는 변수로 사용 불가
        - 되도록이면! 변수명은 의미를 가지게 작성해라
    - degree(변수): 참조하는 이름 → 36.5 → 타입: float, 주소: 491724
    - 거리에 집 주소가 있듯이 메모리의 모든 위치에는 그 위치를 고유하게 식별하는 메모리 주소가 존재
    - 객체(Object)
        - 타입을 갖는 메모리 주소 내 값
        - “값이 들어 있는 상자” → 36.5가 들어있는 상자
    - 할당문: Variable = expression
        - 할당 연산자(=) 오른쪽에 있는 표현식을 평가해서 값(메모리 주소)을 생성
        - 값의 메모리 주소를 ‘=’ 왼쪽에 있는 변수에 저장
        
### 읽기 좋은 코드
- Stlye Guide
    - 코드의 일관성과 가독성을 향상시키기 위한 규칙과 권장사항들의 모음
    - 변수명은 무엇을 위한 변수인지 직관적인 이름을 가져야 함
    - 공백(spaces) 4칸을 사용하여 코드 블록을 들여쓰기(중괄호 안 씀!)
        - 1tap과 4spaces는 다름 그런데 동작 잘 되는 이유? → vscode(에디터)가 내부적 변환
    - 한 줄의 길이는 79자로 제한하며, 길어질 경우 줄 바꿈을 사용
    - 문자와 밑줄(_)을 사용하여 함수, 변수, 속성의 이름을 작성
        - snake_case: 언더바를 섞는 경우
    - 함수 정의나 클래스 정의 등의 블록 사이에는 빈 줄을 추가
    - 연산자와 연산자 사이에는 공백을 넣는 걸 권장
        - result=2+3*(4-5)/2 **(X)**
        - result = 2 + 3 * (4 - 5) **(O)**

### 참고
- [Python Tutor](https://pythontutor.com/): 파이썬 프로그램이 어떻게 실행되는지 도와주는 시각화 도우미
    
    ![img5](https://github.com/goldbutnew/data-marketing-idea-challenge/assets/149566915/0bb2d7a4-5cb7-44c4-b5f0-e566c06480c9)
    
- 주석(Comment)
    - 프로그램 코드 내에 작성되는 설명이나 메모
    - 인터프리터에 의해 실행되지 않음
        - 한 줄 주석: #
        - 여러 줄 주석(docstring?): 3중 따옴표
        - 단축키: Ctrl+/
    - 임시로 코드 비활성화, 코드를 이해하거나 문서화, 다른 개발자나 자신에게 코드의 의도나 동작을 설명
