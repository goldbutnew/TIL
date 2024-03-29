# 제어문 (Control Statement)

- 코드의 실행 흐름을 제어하는 데 사용되는 구문
- 조건에 따라 코드 블록을 실행하거나 반복적으로 코드를 실행

<br>

## 조건문 (Conditional Statement)

- 주어진 조건식을 평가하여 해당 조건이 참(True)인 경우에만 코드 블록을 실행하거나 건너뜀
- 파이썬 조건문에 사용되는 키워드: if / elif / else

### if satatement

- 조건문 기본 구조
    
    ```python
    if 표현식:
    		코드 블록
    elif 표현식:
    		코드 블록
    else: 
    		코드 블록
    ```
    

- 조건문 예시
    1. True
        ```python
        ### TRUE ###
        
        a = 5
        
        if a > 3:
                print('3 초과')
        else:
                print('3 이하')
        
        print(a)
        ```
        ![조건문1](https://github.com/goldbutnew/TIL/assets/149566915/0312598d-4908-41d6-8247-dada32733489)

    2. False
        ```python
        ### FALSE ###
        
        a = 3
        
        if a > 3:
                priint('3 초과')
        else:
                print('3 이하')
        
        print(a)
        ```
        ![조건문2](https://github.com/goldbutnew/TIL/assets/149566915/8f80c1ed-e0c8-4eae-8c2c-024346b16ea5)



- 복수 조건문 예시
    - 조건식을 동시에 검사하는 것이 아니라 순차적으로 비교
        ```python
        dust = 35
        
        if dust > 150:
        		pirnt('매우 나쁨')
        elif dust > 80:
        		print('나쁨')
        elif dust > 30:
        		print('보통')
        else:
        		print('좋음')
        ```
        
    
- 중첩 조건문 예시
    ```python
    if dust > 150:
    		pirnt('매우 나쁨')
    		if dust > 300:
    				print('위험해요! 나가지 마세요!')
    elif dust > 80:
    		print('나쁨')
    elif dust > 30:
    		print('보통')
    else:
    		print('좋음')
    ```
    

<br>

## 반복문 (Loop Statement)
- 주어진 코드 블록을 여러 번 반복해서 실행하는 구문
- for
    - 특정 작업을 반복적으로 수행
    - 종료 조건이 없음
- while
    - 주어진 조건이 참인 동안 반복문
    - 종료 조건이 있음

### for
- 임의의 시퀀스 항목들을 그 시퀀스에 들어가있는 순서대로 반복
- for statement의 기본 구조
    ```python
    for 변수 in 반복 가능한 객체:
    		코드 블록
    ```
- 반복 가능한 객체 (iterable)
    - 반복문에서 순회할 수 있는 객체 (시퀀스 객체 뿐만 아니라 dict, set 등도 포함)
- for 문 원리
    - 리스트 내 첫 항목이 반복 변수에 할당되고 코드 블록이 실행
    - 다음으로 반복 변수에 리스트의 2번째 항목이 할당되고 코드블록이 다시 실행
    - …마지막으로 반복 변수에 리스트의 마지막 요소가 할당되고 코드블록이 실행 
    ```python
    items = ['apple', 'banana', 'coconut']
    
    for item in items:
    		print(item)
    
    """
    apple
    banana
    coconut
    """
    ```
- 문자열 순회
    ```python
    country = 'Korea'
    
    for char in country:
    		print(char)
    
    """
    K
    o
    r
    e
    a
    """
    ```
- range 순회
    ```python
    for i in range (5):
    		print(i)
    
    """
    0
    1
    2
    3
    4
    """
    ```
- 인덱스로 리스트 순회
    - 리스트의 요소가 아닌 인덱스로 접근하여 해당 요소들을 변경하기
    ```python
    numbers = [4, 6, 10, -8, 5]
    
    for i in range(len(numbers)):
    		numbers[i] = numbers[i] * 2
    
    print(numbers)
    
    # [8, 12, 20, -16, 10]
    ```
- 중첩된 반복문
    - 안쪽 반복문이 다 끝나야 위로 넘어가게 됨
    - 안쪽 반복문은 outers 리스트의 각 항목에 대해 한 번씩 실행됨
    - print가 호출되는 횟수 ⇒ len(outers) * len(inners)
    ```python
    outers = ['A', 'B']
    inners = ['c', 'd']
    
    for outer in outers:
    		for inner in inners:
    				print(outer, inner)
    
    """
    A c
    A d
    B c
    B d
    """
    ```
- **중첩 리스트 순회 (2차원 리스트 순회)**
    - 안쪽 리스트 요소에 접근하려면 바깥 리스트를 순회하면서 중첩 반복을 사용해 각 안쪽 반복을 순회 
    ```python
    elements = [['A', 'B'], ['c', 'd']]
    
    for elem in elements:
    		print(elem)
    
    """
    ['A', 'B']
    ['c', 'd']
    """
    ```
    ```python
    elements = [['A', 'B'], ['c', 'd']]
    
    for elem in elements:
    		for item in elem:
    				print(item)
    
    """
    A
    B
    c
    d
    """
    ```
- **중첩 리스트 순회 (2차원 리스트 순회)**
    - 안쪽 리스트 요소에 접근하려면 바깥 리스트를 순회하면서 중첩 반복을 사용해 각 안쪽 반복을 순회
    ```python
    elements = [['A', 'B'], ['c', 'd']]
    
    for elem in elements:
    		print(elem)
    
    """
    ['A', 'B']
    ['c', 'd']
    """
    ```
    ```python
    elements = [['A', 'B'], ['c', 'd']]
    
    for elem in elements:
    		for item in elem:
    				print(item)
    
    """
    A
    B
    c
    d
    """
    ```
- while
    - 주어진 조건식이 참(True)인 동안 코드를 반복해서 실행
    - ==조건식이 거짓(False)가 될 때까지 반복
- While statemet의 기본 구조
    ```python
    while 조건식:
    			코드 블록
    ```
- while 반복문 예시
    ```python
    a = 0
    
    while a < 3:
    		print(a)
    		a += 1
    
    print('끝')
    
    """
    0
    1
    2
    끝
    """
    ```
- 사용자 입력에 따른 반복
    - while문을 사용한 특정 입력 값에 대한 종료 조건을 활용하기
    ```python
    number = int(input('양의 정수를 입력해 주세요.:'))
    
    while number <=0:
    	if number < 0:
    		print('음수를 입력했습니다.')
    	else:
    		print('0은 양의 정수가 아닙니다.')
    
    	number = int(input('양의 정수를 입력해 주세요.:'))
    
    print('잘했습니다!')
    
    """"
    양의 정수를 입력해 주세요.: 0
    0은 양의 정수가 아닙니다.
    양의 정수를 입력해 주세요: -1
    음수를 입력했습니다.
    양의 정수를 입력해 주세요.: 1
    잘했습니다!
    """
    ```
- 적절한 반복문 활용하기
    - for
        - 반복 횟수가 명확하게 정해져 있는 경우에 유용
        - 예를 들어 리스트, 튜플, 문자열 등과 같은 시퀀스 형식의 데이터를 처리할 때
    - while
        - 반복 횟수가 불명확하거나 조건에 따라 반복을 종료해야 할 때 유용
        - 예를 들어 사용자의 입력을 받아서 특정 조건이 충족될 때까지 반복

### 반복 제어
- for 문과 while은 매 반복마다 본문 내 모든 코드를 실행하지만 때때로 일부만 실행하는 것이 필요할 때가 있음
- break: 반복을 즉시 중지
- continue: 다음 반복으로 건너뜀
- braek 예시
    - 프로그램 종료 조건 만들기   
        ```python
        number = int(input('양의 정수를 입력해 주세요.:'))
        
        while number <=0:
        	if number == -9999:
        			print('프로그램을 종료합니다.')
        			break
        
        	if number < 0:
        		print('음수를 입력했습니다.')
        	else:
        		print('0은 양의 정수가 아닙니다.')
        
        	number = int(input('양의 정수를 입력해 주세요.:'))
        
        print('잘했습니다!')
        
        """
        양의 정수를 입력해 주세요.: -9999
        프로그램을 종료합니다.
        잘했습니다!
        """
        ```
    - 첫 번째 짝수 찾기
        
        ```python
        numbers = [1, 3, 5, 6, 7, 9, 10, 11]
        found_even = False
        
        for num in numbers:
        		if num % 2 == 0:
        			print('첫 번째 짝수를 찾았습니다:', num)
        			foun_even = True
        			break
        
        if no found_even:
        		print('짝수를 찾지 못했습니다')
        
        """
        첫 번째 짝수를 찾았습니다: 6
        """
        ```
- continue 예시
    - 리스트에서 홀수만 출력하기
    - 현재 반복문의 남은 코드를 건너뛰고 다음 반복으로 넘어감
    ```python
    numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    
    for num in numbers:
    		if num % 2 == 0:
    				continue
    		print(num)
    
    """
    1
    3
    5
    7
    9
    """
    ```
- break와 continue 주의사항
    - break와 continue를 남용하는 것은 코드의 가독성을 저하시킬 수 있음
    - 특정한 종료 조건을 만들어 break을 대신하거나, if문을 사용해 continue처럼 코드를 건너뛸 수도 있음
    - 약간의 시간이 들더라도 가능한 코드의 가독성을 유지하고 코드의 의도를 명확하게 작성하도록 노력하는 것이 중요
    ![컨티뉴주의사항](https://github.com/goldbutnew/TIL/assets/149566915/c892cf89-825f-4c9c-94d6-27f70ddf8737)

### List Comprehensio
- 간결하고 효율적인 리스트 생성 방법
- List Comprehension 구조
    - 들여 쓰기가 없는 한 줄 쓰기
    ```python
    [expression for 변수 in iterable]
    List(expression for 변수 in iterable)
    ```
- List Comprehension 활용
  ![사용전후](https://github.com/goldbutnew/TIL/assets/149566915/3abe1fad-6a63-477c-93af-46e199e4229e)
- [참고] List Comprehension과 if 조건문
    ```python
    [expression for 변수 in iterable if 조건식]
    list(expression for 변수 in iterable if 조건식)
    ```
    

- 정수 1, 2, 3을 가지는 3가지 리스트 만들기 예시
    
    ```python
    numbers = ['1', '2', '3']
    
    # 1. for loop
    new_numbers = []
    for number in numbers:
        new_numbers.append(int(number))
    print(new_numbers) # [1, 2, 3]
    
    # 2. map (당연히 잘 쓸 수 있어야 함)
    new_numbers_2 = list(map(int, numbers))
    print(new_numbers_2) # [1, 2, 3]
    
    # 3. list comprehension
    new_numbers_3 = [int(number) for number in numbers]
    print(new_numbers_3)
    
    # 성능은 일반화가 불가능 (외부요인, 상황)
    # loop & map & comprehension 대부분의 상항에서는 compre가 빠르다
    # 하지만 다른 함수, 내장 함수에 따라 map이 더 빠른 경우도 많았다 
    # 파이썬이 3점대 후반에 for loop 성능에 비약적인 향상이 있었음
    # 그래서 극단적인 차이는 존재하지 않는다
    ```
    

### 💡 Compregension을 남용하지 말자.
- simple is better than complex. keep it simple, stupid.
- 프로그래밍은 우리 프로그램이 어떻게 그 목적을 명확하게 전달하는지에 대한 것
- “작은 효율성에 대해서는, 말하자면 97% 정도에 대해서는, 잊어버려라. 섣부른 최적화는 모든 악의 근원이다.” - 도널드 knuth

<br>

## 참고

### pass
- 아무런 동작도 수행하지 않고 넘어가는 역할
- 문법적으로 문장이 필요하지만 프로그램 실행에는 영향을 주지 않아야 할 때 사용
- 있어 봤자 하는 일 아무것도 없음! 오직 에러를 방지하기 위해서 (continue랑 다름)
- pass 예시
    1. 코드 작성 중 미완성 부분
    2. 조건문에서 아무런 동작을 수행하지 않아야 할 때
    3. 무한 루프에서 조건이 충족되지 않을 때 pass를 사용하여 루프를 계속 진행하는 방법

### enumerate
- enumerate(iterable, start=0)
    - iterable 객체의 각 요소에 대해 인덱스와 함께 반환하는 내장함수
- enumerate 예시