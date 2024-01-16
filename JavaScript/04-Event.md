# 이벤트

- 무언가 일어났다는 신호, 사건
- 웹은 이벤트를 통해 특정 동작을 수행
- 모든 DOM 요소는 이러한 event를 만들어냄
- 또 even를 받고 받은 event를 처리(event handler: 이벤트 처리기)할 수 있음

### event object
- DOM에서 이벤트가 발생했을 때 생성되는 객체
- 이벤트 종류
    - mouse, input, keyboard, touch…

<br> 

## event handler

- 이벤트가 발생했을 때 실행되는 함수
- 사용자의 행동에 어떻게 반응할지를 javascript 코드로 표현한 것

### .addEventListener()
```jsx
EvnetTarget.addEventListener(type, handler)
DOM요소.addEventListener(수신할 이벤트, 콜백 함수)
```
- 대표적인 이벤트 핸들러 중 하나
- 특정 이벤트를 DOM 요소가 수신할 때마다 콜백 함수를 호출
- **대상**에 특정 **Event**가 발생하면, **지정한 이벤트를 받아 할 일**을 등록한다

### .addEventListener(type, handler)

- type
    - 수신할 이벤트 이름
    - 문자열로 작성(ex. click)
- handler
    - 발생한 이벤트 객체를 수신하는 콜백 함수
    - 콜백 함수는 발생한 Event object를 유일한 매개변수로 받음

### addEventListener 활용

- 버튼을 클릭하면 버튼 요소 출력하기
    1. 버튼에 이벤트 처리기를 부착하여 클릭 이벤트가 발생하면 이벤트가 발생한 버튼 정보를 출력
        ```jsx
        // 1. 버튼 선택
        const btn = document.querySelector('#b// 1. 버튼 선택
        const btn = document.querySelector('#btn')
        
        // 콜백함수 작성
        const clickCallbackFunc = function (event) {
          console.log(event)
          console.log(event.target)
          console.log(event.currentTarget)
          console.log(this)
        }
        ```
        
    2. 요소에 addEventListener를 부착하게 되면 내부의 this 값은 대상 요소를 가리키게 됨 (event 객체의 currentTarget 속성 값과 동일)
        ```jsx
        // 2. 버튼에 이벤트 핸들러를 부착
        btn.addEventListener('click', clickCallbackFunc)
        ```
        
### addEventListener의 콜백 함수 특징
- 발생한 이벤트를 나타내는 Event 객체를 유일한 매개변수로 받음
- 아무것도 반환하지 않음

### addEventListenr에서의 화살표 함수 주의사항
- 화살표 함수는 자신만의 this를 가지지 않기 때문에 자신을 포함하고 있는 this를 상속받음

### 버블링(Bubbling)

```html
<form id="form">
  form
  <div id="div">
    div
    <p id="p">p</p>
  </div>
</form>
```

```jsx
const formElement = document.querySelector('#form')
const divElement = document.querySelector('#div')
const pElement = document.querySelector('#p')

const clickHandler1 = function (event) {
  console.log('form이 클릭되었습니다.')
}
const clickHandler2 = function (event) {
  console.log('div가 클릭되었습니다.')
}
const clickHandler3 = function (event) {
  console.log('p가 클릭되었습니다.')
}

formElement.addEventListener('click', clickHandler1)
divElement.addEventListener('click', clickHandler2)
pElement.addEventListener('click', clickHandler3)
```
- 한 요소에 이벤트가 발생하면, 이 요소에 할당된 핸들러가 동작
  ![Untitled](https://github.com/goldbutnew/TIL/assets/149566915/890049fc-f9fc-4e18-9ee3-b753dd91a326)
- 이어서 부모 요소의 핸들러가 동작
  ![Untitled 1](https://github.com/goldbutnew/TIL/assets/149566915/5531ae0b-1df2-42cf-84a2-2ab303b1303e)
- 가장 최상단 조상 요소(document)를 만날 때까지 이 과정이 반복되면서 요소 각각에 할당된 핸들러가 동작
- 이벤트가 제일 깊은 곳에 있는 요소에서 시작해 부모 요소를 거슬러 올라가며 발생하는 것이 마치 물 속 거품과 닮았기 때문
- 가장 안쪽의 <p> 요소를 클릭하면 p → div → form 순서로 3개의 이벤트 핸들러 동작

### 이벤트가 정확히 어디서 발생했는지 접근할 수 있는 방법
- event**.target**
- event**.currentTarget**

### target 속성
- 이벤트가 발생한 가장 안쪽 요소(target)를 참조하는 속성
- 실제 이벤트가 시작된 target 요소
- 버블링이 진행되어도 변하지 않음

### currentTarget 속성
- 현재 요소
- 항상 이벤트 핸들러가 연결된 요소만을 참조하는 속성
- this와 같음

### target 속성과 currentTarget 속성 예시
![Untitled 2](https://github.com/goldbutnew/TIL/assets/149566915/a60cc51c-df47-4059-bf84-e3ac4cf346bf)
- 세 요소 중 가장 최상위 요소인 outerouter 요소에만 이벤트 핸들러가 부착
- 각 요소를 클릭했을 때 event의 target과 currentTarget의 차이 비교
- `target`: 실제 이벤트가 발생하는 요소를 가리킴
- `currentTarget`: 핸들러가 연결된 outerouter 요소를 가리킴
- 핸들러는 outerouter 하나밖에 없지만 이 핸들러에서의 outerouter의 내부 모든 하위 요소에서 발생하는 클릭 이벤트를 잡아내고 있음
- 클릭 이벤트가 어디에서 발생했든 상관없이 outerouter까지 이벤트가 버블링되어 핸들러를 실행시키기 때문

### currentTarget 주의사항
- console.log()로 event 객체를 출력할 경우 currentTarget 키의 값은 null을 가짐
- currentTarget은 이벤트가 처리되는 동안에만 사용할 수 있음
- 대신 console.log(event.currentTarget)을 사용하여 콘솔에서 확인 가능
- currentTarget 이후의 속성 값들은 `target`을 참고해서 사용하기

### .preventDefault
- 이벤트 기본 동작 취소
- 해당 이벤트에 대한 기본 동작을 실행하지 않도록 지정