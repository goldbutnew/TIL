# Event Handling

## v-on

- DOM 요소에 이벤트 리스너를 연결 및 수신

### v-on 구성
`v-on:event="handler"`
- handler 종류
    - Inline handlers: 이벤트가 트리거 될 때 실행될 JS 코드
    - Method handlers: 컴포넌트에 정의된 메서드 이름
- v-on shorthand(약어)
    - @: `@event="handler"`

### Inline handlers
- Inline handlers는 주로 간단한 상황에 사용
    ```jsx
    const count = ref(0)
    ```
    ```html
    <button @click="count++">Add 1</button>
    <p>Count: {{ count }}</p>
    ```

### Method handlers
- Inline handlers로는 불가능한 대부분의 상황에서 사용
    ```jsx
    const name = ref('Alice')
    const myFunc = function (event) {
      console.log(event)
      console.log(event.currentTarget)
      console.log(`Hello ${name.value}!`)
    }
    ```
    ```html
    <button @click="myFunc">Hello</button>
    ```
    ![Untitled](https://github.com/goldbutnew/TIL/assets/149566915/63c41c3e-b243-46d1-8bd9-ba75e16b57aa)
- Method Handlers는 이를 트리거하는 기본 DOM Event 객체를 자동으로 수신
    ```jsx
    const myFunc = function (event) {
      console.log(event)
      console.log(event.currentTarget)
      console.log(`Hello ${name.value}!`)
    }
    ```
    
### Inline Handlers에서의 메서드 호출
```jsx
const greeting = function (message) {
  console.log(message)
}
```
```html
<button @click="greeting('hello')">Say hello</button>
<button @click="greeting('bye')">Say bye</button>
```
- 메서드 이름에 직접 바인딩하는 대신 Inline Handlers에서 메서드를 호출할 수도 있음
- 이렇게 하면 기본 이벤트 대신 사용자 지정 인자를 전달할 수 있음


### Inline Handlers에서 event 인자에 접근하기
```jsx
const warning = function (message, event) {
  console.log(message)
  console.log(event)
}
```
```html
<button @click="warning('경고입니다.', $event)">Submit</button>
```
- Inline Handlers에서 원래 DOM 이벤트에 접근하기
- `$event` 변수를 사용하여 메서드에 전달


### Event Modifiers
```html
<form @submit.prevent="onSubmit">
  <input type="submit">
</form>

<a @click.stop.prevent="onLink">Link</a>
```
- Vue는 v-on에 대한 Event Modifiers를 제공해 `event.preventDefault()`와 같은 구문을 메서드에 작성하지 않도록 함
- `stop`, `prevent`, `self` 등 다양한 modifiers를 제공
- 메서드는 DOM 이벤트에 대한 처리보다는 데이터에 관한 논리를 작성하는 것에 집중
- Modifiers는 chained 되게끔 작성할 수 있으며 이때는 작성된 순서로 실행되기 때문에 작성 순서에 유의


### Key Modifiers
- Vue는 키보드 이벤트를 수신할 때 특정 키에 관한 별도 modifiers를 사용할 수 있음
- 예시: key가 enter일 때만 onSubmit 이벤트를 호출하기
    ```html
    <input @keyup.enter="onSubmit">
    ```