# Basic Syntax
231024

1. 변수
2. 데이터 타입
3. 연산자
4. 조건문
5. 반복문
6. 참고

<br>

# 1. 변수

### 식별자(변수명) 작성 규칙

- 반드시 문자, 달러($) 또는 밑줄(_)로 시작
- 대소문자를 구분
- 예약어 사용 불가: `for`, `if`, `function` 등

---

- 카멜 케이스(camelCase): 변수, 객체. 함수에 사용
- 파스칼 케이스(PascalCase): 클래스, 생성자에 사용
- 대문자 스네이크 케이스(SNAKE_CASE): 상수(constants)에 사용

## 변수 선언 키워드

### let

- 블록 스코프(block scope)를 갖는 지역 변수를 선언
    - 블록 스코프? 이 변수가 영향을 끼치는 범위가 블록 단위다(중괄호)
- 재할당 가능
    
    ```jsx
    let number = 10 // 1. 선언 및 초기값 할당
    number = 20 // 2. 재할당
    ```
    
- 재선언 불가능
    - Uncaught SyntaxError: Identifier 'number' has already been declared (이미 선언됐다!)
    
    ```jsx
    let number = 10 // 1. 선언 및 초기값 할당
    let number = 20 // 2. 재선언 불가능 
    ```
    
- ES6에서 추가

### const

- 블록 스코프를 갖는 지역 변수를 선언
- 재할당 불가능
    - Uncaught TypeError: Assignment to constant variable.
    
    ```jsx
    const number = 10 // 1. 선언 및 초기값 할당
    number = 20 // 2. 재할당 불가능
    ```
    
- 재선언 불가능
    - Uncaught SyntaxError: Identifier 'number' has already been declared
    
    ```jsx
    const number = 10 // 1. 선언 및 초기값 할당
    const number = 20 // 2. 재선언 불가능
    ```
    
- 선언 시 반드시 초기값 설정 필요
    - Uncaught SyntaxError: Missing initializer in const declaration
    
    ```jsx
    const number
    ```
    
- ES6에서 추가

### 블록 스코프 (block scope)

- if, for, 함수 등의 ‘중괄호({}) 내부’를 가리킴
- 블록 스코프를 가지는 변수는 블록 바깥에서 접근 불가능
    
    ```jsx
    let x = 1
    
        if (x === 1) {
          **let x = 2
          console.log(x) // 2**
        }
    
    consoel.log(x) // 1
    ```
    

### 변수 선언 키워드 정리

- 기본적으로 const 사용을 권장
- 재할당이 필요한 변수는 let으로 변경해서 사용
- var는 지양

<br>

# 2. 데이터 타입

### 원시 자료형

- primitive type
- `Number`, `StringBooleanundefinednull`
- 변수에 값이 직접 저장되는 자료형
    - 불변
    - 값이 복사


### 원시 자료형 예시
- 변수에 할당될 때 값이 복사됨
- 변수간에 서로 영향을 미치지 않음

```jsx
const bar = 'bar'
console.log(bar) // bar

bar.toUpperCase()
console.log(bar) // bar
```

```jsx
let a = 10
let b = a
b = 20
console.log(a) // 10
console.log(b) // 20
```

### 참조 자료형
- Reference type
- `Objects` (Object, Array, Function)
- 객체의 주소가 저장되는 자료형
    - 가변
    - 주소가 복사

### 참조 자료형 예시

- 객체를 생성하면 객체의 메모리 주소를 변수에 할당
- 변수 간에 서로 영향을 미침

```jsx
const obj1 = { name: 'Alice', age: 30 }
const obj2 = obj1
obj2.age = 40

console.log(obj1.age) // 40
console.log(obj2.age) // 40
```

## 원시 자료형

### Number

- 정수 또는 실수형 숫자를 표현하는 자료형
    
    ```jsx
    const a = 13
    const b = -5
    const c = 3.14 // float - 숫자 표현
    const d = 2.998e8 // 2.998 * 10^8 = 299,800,000
    const e = Infinity
    const f = -Infinity
    const g = NaN // Not a Number를 나타내는 값 
    ```
    

### String

- 텍스트 데이터를 표현하는 자료형

---

- ‘+’ 연산자를 사용해 문자열끼리 결합
    
    ```jsx
    const firstName = 'Tony'
    const lastName = 'Stack'
    const fullName = firstName + lastName
    
    console.log(fullName) // TonyStark
    ```
    
- 곱셉, 나눗셈, 뺄셈 불가능

---

- Template literals (템플릿 리터럴)
    - 내장된 표현식을 허용하느 문자열 작성방식
    - Backtick(``)을 이용하여. 여러 줄에 걸쳐 문자열을 정의할 수도 있고 JavaScript의 변수를 문자열 안에 바로 연결할 수 있음
    - 표현식은 ‘$’와 중괄호(${expression})로 표기
    - ES6+부터 지원
    
    ```jsx
    const age = 100                                    
    const message = `홍길동은 ${age}세입니다.`
    console.log(message) // 홍길동은 100세입니다. 
    ```
    

### null 과 undefined

**null**

- 변수의 값이 없음을 의도적으로 표현할 때 사용

```jsx
let a = null
console.log(a) // null
```

**undefined**

- 변수 선언 이후 직접 값을 할당하지 않으면 자동으로 할당됨

```jsx
let b
console.log(b) // undefined
```

### Boolean

- true/false
- 조건문 또는 반복문에서 Boolean이 아닌 데이터 타입은 “자동 형변환 규칙”에 따라 true 또는 false로 변환됨
- 자동 형변환
    ![1](https://github.com/goldbutnew/TIL/assets/149566915/64dffbe8-1d2b-4733-a77f-e7c0bdecc5b1)
    

<br>

# 3. 연산자

### 할당 연산자

- 오른쪽에 있는 피연산자의 평가 결과를 왼쪽 피연산자에 할당하는 연산자
- 단축 연산자 지원

```jsx
let a = 0

a += 10
console.log(a) // 10

a -= 3
console.log(a) // 7

a *= 10
console.log(a) // 70

a %= 7
console.log(a) // 0
```

### 증가 & 감소 연산자

- 증가 연산자(++)
    - 피연산자를 증가(1을 더함)시키고 연산자의 위치에 따라 증가하기 전이나 후의 값을 반환
        
        ```jsx
        // 전위 연산자
        let a = 3
        const b = ++a
        console.log(a, b) // 4 4, a는 증가됐기 때문에 4, b는 증가된 값을 반환받아서 4
        
        // 후위 연산자
        let x = 3
        const y = x++
        console.log(x, y) // 4, 3
        ```
        
- 감소연산자(—)
    - 피연산자를 감소(1을 뺌) 시키고 연산자의 위치에 따라 감소하기 전이나 후의 값을 반환
- += 또는 -=와 같이 더 명시적인 표현으로 작성하는 것을 권장

### 비교 연산자

- 피연산자들(숫자, 문자, Boolean 등)을 비교하고 결과값을 boolean으로 반환하는 연산자
    
    ```jsx
    3 > 2 // true
    3 < 2 // false
    
    'A' < 'B' // true
    'Z' < 'a' // true
    '가' < '나' // true
    ```
    

### 동등 연산자(==)

```jsx
console.log(1 == 1) // true
console.log('hello' == 'hello') // true
console.log('1' == 1) // true
console.log(0 == false) // true
```

- 두 피연산자가 같은 값으로 평가되는지 비교 후 boolean 값을 반환
- ‘암묵적 타입 변환’ 통해 타입을 일치시킨 후 같은 값인지 비교
- 두 피연산자가 모두 객체일 경우 메모리의 같은 객체를 바라보는지 판별

### 일치 연산자(===)

```jsx
console.log(1 === 1) // true
console.log('hello' == 'hello') // true
console.log('1' === 1) // false
console.log(0 === 'false') // false
```

- 두 피연산자의 값과 타입이 모두 같은 경우 true를 반환
- 같은 객체를 가리키거나, 같은 타입이면서 같은 값인지를 비교
- 엄격한 비교가 이뤄지며 암묵적 타입 변환이 발생하지 않음
- 일치연산자 사용 권장

### 논리 연산자

- and 연산
    - &&
- or 연산
    - ||
- not 연산
    - !
- 단축 평가 지원

```jsx
true && false // fasle
true && true // true

false || true // true
false || false // false

!true // false

1 && 0 // 0
0 && 1 // 0
4 && 7 // 7
1 || 0 // 1
0 || 1 // 1
4 || 7 // 4

```

<br>

# 4. 조건문

### if

- 조건 표현식의 결과값을 boolean 타입으로 변환 후 참/거짓을 판단

### if 예시

```jsx
const name = 'customer'

    if (name === 'admin') {
      console.log('관리자님 환영해요')
    } else if (name === 'customer') {
      console.log('고객님 환영해요')
    } else {
      console.log(`반갑습니다. ${name}님`)
```

### 조건 (삼항) 연산자

- 세 개의 피연산자를 받는 유일한 연산자
- 앞에서부터 조건문, 물음표(?), 조건문이 참일 경우 실행할 표현식, 콜론(;), 조건문이 거짓일 경우 실행할 표현식이 배치

```jsx
const func1 = function(person) {
  if (person > 17) {
    return 'Yes'
  } else {
    return 'No'
  }
}
```

```jsx
const func2 = function (person) {
  return person > 17 ? 'Yes' : 'No'
}
```

<br>

# 5. 반복문

### while

- 조건문이 참이면 문장을 계속해서 수행
    
    ```jsx
    while (조건문) {
    	// do something
    }
    ```
    
- 예시
    
    ```jsx
    let i = 0
    
    while (i < 6) {
    	console.log(i)
    	i += 1
    }
    ```
    

### for

- 특정한 조건이 거짓으로 판별될 때 까지 반복
    
    ```jsx
    for ([초기문]; [조건문]; [증감문]) {
    	// do something
    }
    ```
    
- 예시
    
    ```jsx
    for (let i = 0; i < 6; i++) {
    	console.log(i)
    }
    ```
    
- for 동작 원리
    ![2](https://github.com/goldbutnew/TIL/assets/149566915/0571909f-bb8c-4f09-b776-d4531c408da6)
    

### for …in

- 객체의 열거 가능한 속성(property)에 대해 반복
    
    ```jsx
    for (variable in objects) {
    	statement
    }
    ```
    
- 예시
    
    ```jsx
    const fruits = { a" 'apple', b: 'banana' }
    
    for (const property in object) {
    	console.log(property) // a, b
    	console.log(object[property]) // apple, banana
    }
    ```
    

### for …of

- 반복 가능한 객체(배열, 문자열 등)에 대한 반복
    
    ```jsx
    for (variable of iterable) {
    	statement
    }
    ```
    
- 예시
    
    ```jsx
    const numbers = [0, 1, 2, 3]
    
    for (const number of numbers) {
    	console.log(number) // 0, 1, 2, 3
    }
    ```
    

### 주의

- `for…in`: object에서만 사용
    - for…in은 배열의 반복자 대신 속성 열거를 사용
    - 정수가 아닌 이름과 속성을 포함하여 열거 가능한 모든 속성을 반환
    - 특정 순서에 따라 인덱스를 반환하는 것을 보장할 수 없음
- `for…of`: object가 아닌 모든 반복 가능한 객체에서 사용

- Array 예시
    
    ```jsx
    const arr = ['a', 'b', 'c']
    
    for (const i in arr) {
    	console.log(i) // 0, 1, 2
    }
    
    for (const i of arr) {
    	console.log(i) // a, b, c
    }
    ```
    

- Object 예시
    
    ```jsx
    const capitals = {
      korea: '서울',
      japan: '도쿄',
      china: '베이징',
    }
    
    for (const capital in capitals) {
      console.log(capital) 
    	// korea japan china
    }
    
    for (const capital of capitals) {
      console.log(capital)
      // TypeEroor: capitals is not iterable
    }
    ```
    

### 반복문 사용 시 const 사용 여부

- for문
    - `for (let i = 0; i < arr.length; i++) {…}`의 경우에는 최초 정의한 i를 “재할당” 하면서 사용하기 때문에 **const를 사용하면 에러 발생**
- for...in, for…of
    - 재할당이 아니라. 매반복마다 다른 속성 이름이 변수에 지정되는 것이므로 **const를 사용해도 에러가 발생하지 않음**
    - 단, const 특징에 따라 블록 내부에서 변수를 수정할 수 없음

### 반복문 종합

![3](https://github.com/goldbutnew/TIL/assets/149566915/0337273d-8e38-41d3-87a8-6691d2f67df0)

<br>

# 6. 참고

### var
- 재할당&재선언 가능
- 함수 스코프를 가짐
- 변수 선언 시 var, const, let 키워드 중 하나를 사용하지 않으면 자동으로 var 선언 됨
- 오류 발생 가능성 때문에 const, let 권장

### 함수 스코프(function scope)

```jsx
function foo() {
	var x = 1
	console.log(x) // 1
}

console.log(x) // ReferenceEroor: x is not defined
```

- 함수의 중괄호 내부
- 함수 스코프를 가지는 변수는 함수 바깥에서 접근 불가능