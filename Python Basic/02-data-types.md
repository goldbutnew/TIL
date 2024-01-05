# 기초문법 2

2023-07-17

### Data Types

- 값의 종류와 그 값에 적용 가능한 연산과 동작을 결정하는 속성
    - 값들을 구분하고 어떻게 다뤄야 하는지 알 수 있음
    - 데이터 타입 값들도 각자에게 적합한 도구를 가짐
    - 변수 의도 파악 용이
    - 잘못된 데이터 타입으로 인한 오류 미리 예방
        
---

### Numeric Types
1. int: 정수 자료형
    - 2진수(binary): 0b
    - 8진수(octal): 0o
    - 16진수(hexadecimal): 0x
2. float: 실수 자료형
    - 프로그래밍 언어에서 float는 실수에 대한 **근삿값**
    - 유한 정밀도
        - 컴퓨터 메모리 용량이 한정돼 있고 한 숫자에 대해 저장하는 용량이 제한됨
        - ex)
            ```python
            # 0.66666666666666666666
            print(2/3)

            # 1.66666666666666666667
            print(5/3)
            ```
            
    - 실수 연산 시 주의사항
        - 컴퓨터는 2진수를 사용, 사람은 10진법을 사용
        - 10진수 0.1은 2진수를 표현하면 0.0001100…이런 식으로 무한 반복
        - 무한대 숫자를 그대로 저장할 수 없어서 10진법의 근사값 저장
        - Floating point rounding error
    - 실 연산 시 해결책
        - 두 수의 차이가 매우 작은 수보다 작은지를 확인하거나 math모듈 활용
            
            ```python
            a = 3.2 - 3.1 # 0.10000000000000009
            b = 1.2 - 1.1 # 0.09999999999999987
            ```
            
        - 임의의 작은 수 활용:
            
            ```python
            print(abs(a-b) <= 1e-10) # True
            ```
            
        - math 모듈 활용:
            
            ```python
            import math
            print(math.isclose(a.b)) # True 
            ```
            
    - 지수 표현 방식
        - e 또는 E를 사용한 지수 표현
            
            ```python
            # 314 * 0.01
            number =314e-2
            
            # float 
            print(type(number))
            
            # 3.14
            print(number)
            ```
                
---

### Sequence Types
* 여러 개의 값들이 순서대로 나열하여 저장하는 자료형
    > **순서(Sequence)**
    > 
    > - 값들이 순서대로 저장(정렬 X)
    > 
    > **인덱싱(Indexing)**
    > 
    > - 각 값에 고유한 인덱스(번호)를 가지고 있음
    > - 인덱스를 사용하여 특정 위치의 값을 선택하거나 수정할 수 있음
    > - 1이 아닌 0부터 시작함(프로그래밍 언어는 대부분 0부터 시작)
    > 
    > **슬라이싱(Slicing)**
    > 
    > - 인덱스 범위를 조절해 부분적인 값을 추출할 수 있음
    > 
    > **길이(Length)**
    > 
    > - len() 함수를 사용하여 저장된 값의 개수(길이)를 구할 수 있음
    > 
    > **반복(lteration)**
    > 
    > - 반복문을 사용하여 저장된 값들을 반복적으로 처리할 수 있음
        
    - str: 문자들의 순서가 있는 변경 불가능한 시퀀스 자료형
        - 문자열 표현
            - 문자열은 단일 문자나 여러 문자의 조합으로 이루어짐
            - 작은 따옴표(’) 또는 큰따옴표(”) 감싸서 표현
        - 중첩 따옴표
            - 따옴표 안에 따옴표를 표현할 경우
            - 작은 따옴표가 들어 있는 경우는 큰따옴표로 문자열 생성
            - 큰따옴표가 들어 있는 경우는 작은 따옴표로 묶는다
        - Escape sequence
            - 역슬래시 뒤에 특정 문자가 와서 특수한 기능을 하는 문자 조합
            - 파이썬의 일반적인 문법 규칙을 잠시 탈출한다는 의미
                
                ![escape_sequence](https://github.com/goldbutnew/TIL/assets/149566915/76065111-93bc-47e8-9719-eb11bfc4baab)
                
            - ex)
                
                ```python
                # 철수야 '안녕'
                print('철수야 \'안녕\'')
                
                ```
                이 다음은 엔터
                입니다.
                ```
                pirnt('이 다음은 엔터\n입니다.')
                ```
                
    - String Interpolation(보관법): 문자열 내에 변수나 표현식을 삽입하는 방법
        - f-string
            - 문자열에 f 또는 F 접두어를 붙이고 표현식을 {expression}로 작성하여 문자열에 파이썬 표현식의 값을 삽입할 수 있음
            
            ```python
            bugs = 'roaches'
            counts = 13
            area = 'living room'
            
            # Debugging roaches 13 living room
            print(f'Debugging {bugs} {counts} {area}')
            ```
            
        - 문자열 시퀀스의 특징
            
            ```python
            my_str = 'hello'
            
            # 인덱싱
            print(my_str[1]) # e
            
            # 슬라이싱
            print(my_str[2:4]) # 11
            
            # 길이
            print(len(my_str)) # 5
            ```
            
    - 인덱스(index): 시퀀스 내의 값들에 대한 고유한 번호로, 각 값의 위치를 식별하는 데 사용되는 숫자 (강의 다시보기 하셈…..)
        - ex)
            
            ![%EC%9D%B8%EB%8D%B1%EC%8A%A4%EC%98%88%EC%8B%9C](https://github.com/goldbutnew/TIL/assets/149566915/407af66e-06ca-42b9-b4b8-c635401eca3f)
    
    - 슬라이싱(slicing): 시퀀스의 일부분을 선택하여 추출하는 작업 → 시작 인덱스와 끝 인덱스를 지정하여 해당 범위의 값을 포함하는 새로운 시퀀스를 생성
        - slicing 예시
            
            <Tip: 인덱스 기준을 문자 위치가 아닌 문자 사이의 공백으로 보는 걸 추천>
            
            - `my_str[2:4]`
                
                ![1](https://github.com/goldbutnew/TIL/assets/149566915/139f7641-a519-4c03-86ec-a04d7249f193)
                
            - `my_str[:3]`
                
                ![2](https://github.com/goldbutnew/TIL/assets/149566915/daddbda5-853c-4585-88f4-46e8e260f0ac)
                
            - `my_str[3:]`
                
                ![3](https://github.com/goldbutnew/TIL/assets/149566915/1ab97d31-b7bb-4aaa-9831-0ca7c5c6bef1)
                
        - step을 지정하여 추출
            - `my_str[0:5:2]`
                
                ![4](https://github.com/goldbutnew/TIL/assets/149566915/eba6e6dc-87e6-48f7-991c-06340eed84ec)

        - step이 음수일 경우
            - `my_str[::-1]`
                
                ![5](https://github.com/goldbutnew/TIL/assets/149566915/b023bc87-bdd3-4583-8b0b-e07947b933a8)
                
        - 문자열은 불변 (변경 불가)
            
            ```python
            my_str = 'hello'
            
            #TypeError: 'str' object does not support item assignment
            mystr[1] = 'z'
            ```
            
            - 문자열을 바꾸려고 할 생각 대신 새로운 문자열을 만든다는 생각으로 접근
            
    - list(리스트): 여러 개의 값을 순서대로 저장하는 변경 가능한 시퀀스 자료형 → 문자열과 다 같은데 변경 가능하다는 점이 다름
        - 리스트 표현
            
            ```python
            my_list_1 = []
            my_list_2 = [1, 'a', 3, 'b', 5]
            my_list_3 = [1, 2, 3, 'Python', ['hello', 'world', '!!!']]
            ```
            
            - 0개 이상의 객체를 포함하며 데이터 목록을 저장
            - 대괄호([])로 표기
            - 데이터는 어떤 자료형도 저장할 수 있음
        - 리스트 시퀀스 특징
            
            ```python
            my_list = [1, 'a', 3, 'b', 5]
            
            # 인덱싱
            print(my_list[1]) # a
            
            # 슬라이싱
            print(my_list[2:4]) # [3, 'b']
            print(my_list[:3]) # [1, 'a', 3]
            print(my_list[3:]) # ['b', 5]
            print(my_list[0.5:2]) # [1, 3, 5]
            print(my_list[::-1]) # [5, 'b', 3, 'a', 1]
            
            # 길이
            print(len(my_list)) # 5
            ```
            
        - 중첩된 리스트 접근
            
            ```python
            my_list = [1, 2, 3, 'Python', ['hello', 'world', '!!!']]
            
            print(len(my_list)) # 5
            print(my_list[4][-1]) # !!!
            print(my_list[-1][1][0]) # w
            ```
            
        - 리스트는 가변 (변경 가능)
            
            ```python
            my_list = [1, 2, 3]
            my_list[0] = 100
            
            print(my_list) # [100, 2, 3]
            ```
            
        - 누구는 ‘객체들의 참조를 모아둔 컬렉션’이라고 부르기도 함
    
    - tuple(튜플): 여러 개의 값을 순서대로 저장하는 변경 불가능한 시퀀스 자료형
        - 튜플 표현
            
            ```python
            my_tuple_1 = ()
            my_tuple_2 = (1,)
            my_tuple_3 = (1, 'a', 3, 'b', 5)
            ```
            
            - 0개 이상의 객체를 포함하며 데이터 목록을 저장
            - 소괄호(())로 표기
            - 데이터는 어떤 자료형도 저장할 수 있음
        - 튜플의 시퀀스 특징
            
            ```python
            my_tuple = (1, 'a', 3, 'b', 5)
            
            # 인덱싱
            print(my_tuple[1]) # a
            
            # 슬라이싱
            print(my_tuple[2:4]) # (3, 'b')
            print(my_tuple[:3]) # (1, 'a', 3)
            print(my_tuple[3:]) # ('b', 5)
            print(my_tuple{0:5:2}) # (1, 3, 5)
            print(my_tuple[::-1}) # (5, 'b', 3, 'a', 1)
            
            # 길이
            print(len(my_tuple)) # 5
            ```
            
        - 튜플은 불변 (변경 불가)
            
            ```python
            my_tuple = (1, 'a', 3, 'b', 5)
            
            # TypeError: 'tuple' object does not support item assignment
            my_tuple[1] = 'z'
            ```
            
        - 튜플은 어디에 쓰일까?
            - 튜플의 불변 특성을 사용한 안전하게 여러 개의 값을 전달, 그룹화 다중할당 등 개발자가 직접 사용하기보다 ‘파이썬 내부 동작’에서 주로 사용됨
            
            ```python
            x, y = (10, 20)
            print(x) # 10
            print(y) # 20
            
            # 파이썬은 쉼표를 튜플 생성자로 사용하니 괄호는 생략 가능
            x,y = 10, 20
            ```
            
    - Range: 연속된 정수 시퀀스를 생성하는 변경 불가능한 자료형
        - range(n)
            - 0부터 n-1까지의 숫자 시퀀스
        - range(n, m)
            - n부터 m-1까지의 숫자 시퀀스
                
                ```python
                my_range_1 = range(5)
                my_range_2 = range(1, 10)
                
                print(my_range_1) # range(0, 5)
                print(my_range_2) # range(1, 10)
                ```
                
            - 주로 반복문과 함께 사용 예정
                
                ```python
                # 리스트로 형 변환 시 데이터 확인 가능
                print(list(my_range_1)) # [0, 1, 2, 3, 4]
                print(list(my_range_2)) # [1, 2, 3, 4, 5, 6, 7, 8, 9]
                ```
                
    
    1. **Non-sequence Types**
        - dict(딕셔너리)
            - key-value 쌍으로 이루어진 순서와 중복이 없는 변경 가능한 자료형
            - 딕셔너리 표현
                - key는 변경 불가능한 자료형만 사용 가능 (str, int, float, tuple, range…)
                - value는 모든 자료형 사용 가능
                - 중괄호({})로 표기
                
                ```python
                my_dict_1 = {}
                my_dict_2 = {'key': 'value'}
                my_dict_3 = {'apple': 12, 'list': [1, 2. 3]}
                
                print(my_dict_1) # {}
                print(my_dict_2) # {'key': 'value'}
                print(my_dict_3) # {'apple': 12, 'list': [1, 3, 3]}
                ```
                
            - 딕셔너리 사용
                - key를 통해 vlaue에 접근
        - set(세트)
            - 순서와 중복이 없는 변경 가능한 자료형
            - 세트 표현
                - 수학에서의 집합과 동일한 연산 처리 가능
                - 중괄호({})로 표기 → dict과 set 둘 다 중괄호 표기
                    - 빈 딕셔너리/세트 만들 때: my_dict_1={} / my_set_1= set()
                
                ```python
                my_set_1 = set()
                my_set_2 = {1, 2, 3}
                my_set_3 = {1, 1, 1}
                
                print(my_set_1) # set()
                print(my_set_2) # {1, 2, 3}
                print(my_set_3) # {1}
                
                ---
                
                my_set_1 = {1, 2, 3}
                my_set_2 = {3, 6, 9}
                
                # 합집합
                print(my_set_1 | my_set_2) # {1, 2, 3, 6, 9}
                
                # 차집합
                print(my set_1 - my_set_2) # {1, 2}
                
                # 교집합
                print(my_set_1 & my_set_2) # {3}
                ```
                
                - 순서가 없어서 index가 없음
                
        - None
            - 파이썬에서 ‘값이 없음’을 표현하는 자료형
                
                ```python
                variable = None
                print(variable) # None
                ```
                
        
        - Bloean
            
            ```python
            bool_1 = True
            bool_2 = Fales
            
            print(bool_1) # True
            pirnt(bool_2) # False
            print(3 > 1)( # True
            print('3' != 3) # True
            ```
            
            - 참과 거짓을 표현하는 자료형
            - 비교/논리 연산의 평가 결과로 사용됨
            - 주로 조건/반복문과 함께 사용

---

### Collection
* 여러 개의 항목 또는 요소들을 담는 자료 구조 (str, list, tuple, set, dict)
- 컬렉션 정리
    ![summury](https://github.com/goldbutnew/TIL/assets/149566915/20f76346-dfa1-4220-a36a-4f2844d95284)
    
    정렬 → 순서 (오타)
    
- 불변과 가변의 차이
    
    ```python
    # 불변과 가변의 차이
    my_str = 'hello'
    
    # TypeError: 'str' object does not support item assignment
    my_str[0] = 'z'
    
    my_list = [1, 2, 3]
    my_list[0] = 100
    
    # [100, 2, 3]
    print(my_list)
    
    list_1 = [1, 3, 4]
    list_2 = list_1
    list1[0] = 100
    print(list_1) # [100, 2, 3]
    pritn(list_2) # [100, 2, 3]
    ```
    
    ![tutor](https://github.com/goldbutnew/TIL/assets/149566915/22c70a30-e2a7-4261-a606-64abe1e1b3bd)
        
---

### Type Conversion
* 암시적 형변환(Implict Type conversion)
    - 파이썬이 자동으로 형변환을 하는 것
    - 참과 거짓을 평가할 때 많이 사용됨
        - 특히 if문에서 참거짓 판별해서 동작할 때
        - 판단할 때만 형변환, 값 자체를 바꾸지는 않음
        - 값이 있으면 true, 비어 있으면 false
    - 암시적 형변환의 예시
        - Boolean과 Numeric Type에서만 가능
            
            ```python
            print(3 + 5.0) # 8.0
            print(True + 3) # 4 # true과 1이고 false과 0
            print(True + False) # 1
            ```
            
        - 더 다양한 값의 범위를 표현하기 위해서 암시적인 형 변환이 이루어진다
        
* 명시적 형변환(Explict Type conversion)
    - 개발자가 직접 형변환을 하는 것
    - 암시적 형변환이 아닌 경우를 모두 포함
    - 명시적 형변환 예시
        - str → integer: 형식에 맞는 숫자만 가능
        - integer → str: 모두 가능
            
            ```python
            print(int('1')) # 1
            print(str(1) + '등') # 1등
            print(float('3.5')) # 3.5
            print(int(3.5)) #3
            
            # a ValueError: invaild literal for int() with base 10: '3.5'
            # 실수형 문자를 정수형으로 바꾸려고 하면 에러 발생
            print(int('3.5'))
            ```
                
    
    - 컬렉션 간 형변환 정리
        ![conversion](https://github.com/goldbutnew/TIL/assets/149566915/de8339f8-04aa-42be-89b4-ff2ec538dca4)
    
---

### Operator
* 연산자
    - 산술 연산자
        ![operator](https://github.com/goldbutnew/TIL/assets/149566915/be39a524-8ed7-48c6-98d1-b544a085e9c1)
        
    - 복합 연산자
        - 연산과 할당이 함께 이뤄짐
        - 복합 연산자 예시
    - 비교 연산자
        - is 비교 연산자
        - ==는 동등성(equality), is는 식별성(identity)
        - 값을 비교하는 ==와는 다름
        - is: 같음 / is not: 같지 않음
        
        ```python
        2.0 == 2 (T)
        2.0 is 2 (F)
        
        a = 256
        b = 256
        a is b (T)
        
        c = 257
        d = 257
        c is d (F) # 257부터 값은 같더라도 다른 객체를 가리켜서 c와 d는 메모리값이 다름
        
        a = [1, 2, 3]
        b = a
        a is b (T)
        
        a = [1, 2, 3]
        b = [1, 2, 3]
        a is b (F) 
        ```
        

    - 논리 연산자
        - and: 논리곱 / 두 피연산자 모두 True인 경우에만 전체 표현식을 True로 평가
        - or: 논리합 / 두 피연산자 중 하나라도 True인 경우 전체 표현식을 True로 평가
        - not: 논리부정 / 단일 피연산자를 부정
        - 논리 연산자 예시
            
            ```python
            print(True and False) # False
            
            print(True and False) # True
            
            print(not True) # False
            
            print(not 0) # True
            ```
            
        - 비교 연산자와 함께 사용 가능
            
            ```python
            num = 15
            ```
            
    - 단축 평가
        - 논리 연산에서 두 번째 피연산자를 평가하지 않고 결과를 결정하는 동작
        - 단축평가 예시
            
            ```python
            vowels = 'aeiou'
            
            print(('a' and 'b') in vowels) # False
            print(('b' and 'a') in vowels) # True
            
            print(3 and 5) # 5
            print(3 and 0) # 0
            print(0 and 3) # 0
            print(0 and 0) # 0
            
            print(5 or 3) # 5
            print(3 or 0) # 3
            print(0 or 3) # 3
            print(0 or 0) # 0 
            ```
            
        - 단축평가 동작 jjh y
            - and
                - 첫 번째 피연산자가 False인 경우, 전체 표현식 False로 결정
                - 두 번째 피연산자는 평가되지 않고 그 값이 무시
                - 첫 번째 피연산자가 True인 경우, 전체 표현식의 결과는 두 번째 피연산자에 의해 결정
                - 두 번째 피연산자가 평가되고 그 결과가 전체 표현식의 결과로 반환
            - or
                - 첫 번째 피연산자가 T인 경우, 전체 표현식은 True로 결정
                - 두 번째 피연산자는 평가되지 않고 그 값이 무시
                - 첫 번째 피연산자가 False인 경우, 전체 표현식의 결과는 두 번째 피연산자에 의해 결정
                - 두 번째 피연산자가 평가되고 그 결과가 전체 표현식의 결과로 반환
                
    - 멤버십 연산자
        - 특정 값이 시퀀스나 다른 컬렉션에 속하는지 여부를 확인
        - in: 왼쪽 피연산자가 오른쪽 피연산자의 시퀀스에 속하는지를 확인
        - not in: 왼쪽 피연산자가 오른쪽 피연산자의 시퀀스에 속하지 않는지를 확인
        - 멤버십 연산자 예시
            
            ```python
            word = 'hello'
            numbers = [1, 2, 3, 4, 5]
            
            print('h', in word) # True
            print('z', in word) # False
            
            print(4 not in numbers) # False
            print(6 not in numbers) # True
            ```
            
    - 시퀀스형 연산자
        - +와 *는 시퀀스 간 연산에서 산술 연산자일 때와 다른 역할을 가짐
        - +: 결합 연산자
        - *: 반복 연산자
        - 시퀀스 연산자 예시
            
            ```python
            # Gildong Hong
            print('Gildong' + 'Honh')
            
            # hihihihihi
            print('hi' * 5)
            
            # [1, 2, 'a', 'b']
            print([1, 2] + ['a', 'b'])
            
            # [1, 2, 1, 2]
            print([1, 2] * 2)
            ```
            
    - 연산자 우선순위
        ![operator2](https://github.com/goldbutnew/TIL/assets/149566915/f0264808-aff9-437c-b83f-68e9773a6de4)