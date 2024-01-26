# Form Input Binding
- form을 처리할 때 사용자가 input에 입력하는 값을 실시간으로 JS 상태에 동기화해야 하는 경우 (양방향 바인딩)
- 양방향 바인딩 방법
    1. `v-bind`와 `v-on`을 함께 사용
    2. `v-model` 사용

### v-bind와 v-on을 함께 사용
```jsx
const inputText1 = ref('')
const onInput = function (event) {
  **inputText1.value = event.currentTarget.value**
}
```
```html
<p>{{ inputText1 }}</p>
<input :value="inputText1" @input="onInput">
```
- `v-bind`를 사용하여 input 요소의 value 속성값을 입력값으로 사용
- `v-on`을 사용하여 input 이벤트가 발생할 때마다 input 요소의 value 값을 별도 반응형 변수에 저장하는 핸들러 호출

### v-model
```jsx
const inputText2 = ref('')
```
```html
<p>{{ inputText2 }}</p>
<input v-model="inputText2">
```
- form input 요소 또는 컴포넌트에서 양방향 바인딩을 만듦
- IME가 필요한 언어의 경우 v-model 제대로 업데이트되지 않아서 그때는 v-bind와 v-on 방법을 사용해야 함

## v-model과 다양한 입력(input) 양식
- v-modle은 단순 text input 뿐 아니라 Checkbox, Radio, Select 등 다양한 타입의 사용자 입력 방식과 함께 사용 가능

### Checkbox 활용
- 단일 체크박스와 boolean 활용
    ```jsx
    const checked = ref(false)
    ```
    ```html
    <input type="checkbox" id="checkbox" v-model="checked">
    <label for="checkbox">{{ checked }}</label>
    ```
- 여러 체크박스와 배열 활용
    ```jsx
    const checkeNames = ref([])
    ```
    ```html
    <div>Checked names: {{ checkeNames }}</div>
    
    <input type="checkbox" id="alice" value="Alice" v-model="checkeNames">
    <label for="alice">Alice</label>
    
    <input type="checkbox" id="bella" value="Bella" v-model="checkeNames">
    <label for="bella">Bella</label>
    ```
    - 해당 배열에는 현재 선택된 체크박스의 값이 포함됨

### Select 활용
- select에서 v-model 표현식의 초기값이 어떤 option과도 일치하지 않는 경우 select 요소는 **선택되지 않은(unselected)** 상태로 렌더링 됨
    ```jsx
    const selected = ref('')
    ```
    
    ```jsx
    <select v-model="selected">
      <option disabled value="">Please select one</option>
      <option>Alice</option>
      <option>Bella</option>
      <option>Cathy</option>
    </select>
    ```