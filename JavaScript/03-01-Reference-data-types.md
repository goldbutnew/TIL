# 함수
- Function
- 참조 자료형에 속하며 모든 함수는 Function object
    - 참조 자료형이란? 객체의 주소가 저장되는 자료형(가변, 주소가 복사)

<br>

## 함수 정의

### 함수 구조
- 함수의 이름
- 함수의 매개변수
- 함수의 body를 구성하는 statement
- return 값이 없다면 undefined를 반환
    ```jsx
    function name([params[, params,[..., params]]]) {
        statements
        return value
    }
    ```
    

### 함수의 정의 2가지 방법

<aside>
- 선언식
    - function declaration
        ```jsx
        function funcName () {
            statements
        }
        ```
        ```jsx
        function add(num1, num2) {
            return num1 + num2
        }

        add(1, 2) // 3
        ```
</aside>

<aside>
- 표현식
    - function expression
        ```jsx
        const funcName = function () {
            statements
        }
        ```
        ```jsx
        const sub = function (n1, n2) {
            return n1 - n2
        }

        sub(2, 1) // 1
        ```
</aside>

### 함수 표현식 특징

- 함수 이름이 없는 ‘익명 함수’를 사용할 수 있음
- 선언식과 달리 표현식으로 정의한 함수는 호이스팅이 되지 않으므로 함수를 정의하기 전에 먼저 사용할 수 없음 → 초기값(initialization) 선언 필요
```jsx
// 선언식

add (1, 2) // 3

function add(num1, num2) {
    return num1 + num2
}
```
```jsx
// 표현식 

add (1, 2)
// ReferenceError

const sub = function (n1, n2) {
    return n1 - n2
}
```

<br>

## 매개 변수

### 기본 함수 매개 변수
- default function parameter
- 값이 없거나 undefined가 전달될 경우 이름 붙은 매개변수를 기본값으로 초기화

### 나머지 매개변수
- Rest parameters
- 임의의 수의 인자를 ‘배열’로 허용하여 가변 인자를 나타내는 방법

### 매개변수와 인자의 개수 불일치
- 매개변수 개수 > 인자 개수
    - 누락된 인자는 undefiend로 할당
    ```jsx
    const threeArgs = function (num1, num2, num3) {
      return [num1, num2, num3]
    }
    
    console.log(threeArgs()) // [undefiend, undefiend, undefiend]
    console.log(threeArgs(1)) // [1, undefiend, undefiend]
    console.log(threeArgs(2, 3)) // [2, 3, undefiend]
    ```
- 매개변수 개수 < 인자 개수
    - 초과 입력한 인자는 사용하지 않음
    ```jsx
    const noArgs = function () {
      return 0
    }
    
    console.log(noArgs(1, 2, 3)) // 0
    
    const twoArgs = function (num1, num2) {
      return [num1, num2]
    }
    
    console.log(twoArgs(1, 2, 3)) // [1, 2]
    ```

<br>

## Spread syntax
- `...`
- 전개 구문
- 배열이나 문자열과 같이 반복 가능한 항목을 펼치는 것 (확장, 전개)
- 전개 대상에 따라 역할이 다름
    - 함수와의 사용
        - 함수 호출 시 인자 확장
        - 나머지 매개변수 (압축)
    - 객체와의 사용
    - 배열과의 사용

### 전개 구문 활용
- 함수와의 사용
    - 함수 호출 시 인자 확장
        ```jsx
        function myFunc(x, y, z) {
          return x + y + z
        }
        
        let numbers = [1, 2, 3]
        
        console.log(myFunc(**...**numbers)) // 6
        ```
    - 나머지 매개 변수(압축)
        
        ```jsx
        function myFunc2(x, y, **...**restArgs) {
          return [x, y, restArgs]
        }
        
        console.log(myFunc2(1, 2, 3, 4, 5)) // [1, 2, [3, 4, 5]]
        console.log(myFunc2(1, 2)) // [1, 2, []]
        ```

<br>

## 화살표 함수
- Arrow function expressions
- 함수 표현식의 간결한 표현법

### 화살표 함수 작성 결과
```jsx
const arrow = function (name) {
	return `hello, ${name}`
}
```
↓
```jsx
const arrow = name => `hello, ${name}`
```

### 화살표 함수 작성 결과
1. function 키워드 제거 후 매개변수와 주오갈호 사이에 화살표 `⇒` 작성
    ```jsx
    const arrow1 = function (name) {
      return `hello, ${name}`
    }
    
    // 1. function 키워드 삭제 후 화살표 작성
    const arrow2 = (name) => { return `hello, ${name}` }
    ```
2. 함수의 매개변수가 하나 뿐이라면, 매개변수의 `()` 제거 가능 (단, 생략하지 않는 것을 권장)
    ```jsx
    // 2. 인자가 1개일 경우에만 () 생략 가능
    const arrow3 = name => { return `hello, ${name}` }
    ```
3. 함수 본문의 표현식이 한 줄이라면, `{}` 와 `return` 제거 가능 
    ```jsx
    // 3. 함수 본문이 return을 포함한 표현식 1개일 경우에 {} & return 삭제 가능
    const arrow4 = name => `hello, ${name}`
    ```
    
### 화살표 함수 심화
1. 인자가 없다면 `()` or `_` 로 표시 가능
    ```jsx
    const noArgs1 = () => 'No args'

    const noArgs2 = _ => 'No args'
    ```
2. object return
    1. return을 명시적으로 작성해야 함
        
        ```jsx
        const returnObject1 = () => {return { key: 'value' }}
        ```
        
    2. return을 작성하지 않으려면 객체를 소괄호로 감싸야 함
        
        ```jsx
        const returnObject2 = () => ({ key: 'value' })
        ```