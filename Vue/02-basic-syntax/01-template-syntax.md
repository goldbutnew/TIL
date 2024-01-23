# Template Syntax

- DOM을 기본 구성 요소 인스턴스의 데이터에 선언적으로 바인딩(Vue Instance와 DOM을 연결)할 수 있는 HTML 기반 템플릿(확장된 문법 제공)구문을 사용

<br>

## Template Syntax 종류

### Text Interpolation
```html
<p>message: {{ msg }}</p>
```
- 데이터 바인딩의 가장 기본적인 형태
- 이중 중괄호 구문 (콧수염 구문)을 사용
- 콧수염 구문은 해당 구성 요소 인스턴스의 msg 속성값으로 대체
- msg 속성이 변경될 때마다 업데이트 됨

### Raw HTML
```html
<div v-html="rawHtml"></div>
```
```jsx
const rawHtml = ref('<span style="color:red">This should be red.</span>')
```
- 콧수염 구문은 데이터를    ****로 해석하기 때문에 실제 HTML을 출력하려면 v-html을 사용해야 함

### Attribute Bindings
```html
<div v-bind:id="dynamicId"></div>
```
```jsx
const dynamicId = ref('my-id')
```
- 콧 수염 구문은 HTML 속성 내에서 사용할 수 없기 때문에 `v-bind`를 사용
- HTML id 속성값을 vue의 dynamicId 속성과 동기화 되도록 함
- 바인딩 값이 null이나 undefind인 경우 렌더링 요소에서 제거

### JavaScript Expressions
```html
<div>{{ number + 1 }}</div>
<div>{{ ok ? 'Yes' : 'No' }}</div>
<div>{{ msg.split('').reverse().join('') }}</div>
<div v-bind:id="`list-${id}`"></div>
```
- Vue는 모든 데이터 바인딩 내에서 JS 표현식의 모든 기능 지원
- Vue 템플릿에서 JS 표현식을 사용할 수 있는 위치
    - 콧수염 구문 내부
    - 모든 directive의 속성값 (v-로 시작하는 특수 속성)

### Expressions 주의사항
- 각 바이딩에는 하나의 단일 표현식만 포함될 수 있음
    - 표현식은 값으로 평가할 수 있는 코드 조각 (return 뒤에 사용할 수 있는 코드여야 함)
- 작동하지 않는 경우
    ```html
    <!-- 표현식이 아닌 선언식 -->
    {{ const number = 1 }}
    
    <!-- 흐름제어도 작동하지 않음. 삼항 표현식 사용 -->
    {{ if (ok) { return message } }}
    ```
    
<br>

## Directive
- `v-` 접두사가 있는 특수 속성

### Directive 특징
- Directive의 속성값은 단일 JS 표현식이어야 함 (v-for, v-on 제외)
- 표현식 값이 변경될 때 DOM에 반응적으로 업데이트 적용
- 예시
    - v-if는 seen 표현식 값의 T/F를 기반으로 <p>요소를 제거/삽입
    ```jsx
    <p v-if="seen">Hi There</p>
    ```
    
### Directive 전체 구문
![Untitled](https://github.com/goldbutnew/TIL/assets/149566915/dc096f94-9e9d-4a2a-8e4a-15d1d27946c2)

### Directive - Argument
- **일부** directive는 directive 뒤에 콜론(:)으로 표시되는 인자를 사용할 수 있음
- 아래 예시의 href는 HTML a요소의 href 속성 값을   myUrl 값에 바인딩 하도록 하는 v-bind의 인자
    ```html
    <a v-bind:href="myUrl">Link</a>
    ```
- 아래 예시의 click은 이벤트 수신할 이벤트 이름을 작성하는 v-on의 인자
    ```html
    <button v-on:click="doSomething">버튼</button>
    ```
    
### Directive - Modifiers
- .(dot)로 표시되는 특수 접미사로, directive가 특별한 방식으로 바인딩되어야 함을 나타냄
- 예를 들어 .prevent는 발생한 이벤트에서 event.preventDefault()를 호출하도록 v-on에 지시하는 modifier (잠깐! 개념 복습: event.preventDefault는 페이지 새로고침 등 JS기본 동작을 하지 않도록 하는 함수)
    ```html
    <form v-on:submit.prevent="onSubmit">
      <input type="submit">
    </form>
    ```
    
### Built-in Directives
- v-text
- v-show
- v-if
- v-for
- …