# v-bind

- 하나 이상의 속성 또는 컴포넌트 데이터를 표현식에 동적으로 바인딩
- Attribute Bindings와 Class and Style Bindings에서 사용

<br>

## Attribute Bindings

- HTML 속성값을 Vue의 상태 속성 값과 동기화되도록 함
    ```html
    <img v-bind:src="imageSrc" alt="">
    <a v-bind:href="myUrl">Link</a>
    ```
    - v-bind shorthand(약어)
        - `:` (colon)
    - HTML에 사용되는 모든 속성값을 인자로 받을 수 있음
- Dynamic attribute name (동적 인자 이름)
    ```html
    <p :[dynamicattr]="dynamicValue">........</p>
    ```
    - 대괄호로 감싸서 directive argument에 JS 표현식을 사용할 수도 있음
    - JS 표현식에 따라 동적으로 평가된 값이 최종 argumnet 값으로 사용됨
    - **대괄호 안에 작성하는 이름은 반드시 소문자로만 구성 가능** (카멜케이스 쓰면 안 됨!!! 브라우저가 속성 이름을 소문자로 강제 변환)

### Attribute Bindings 예시
```html
<img v-bind:src="imageSrc" alt="">
<a v-bind:href="myUrl">Link</a>
<p :[dynamicattr]="dynamicValue">........</p>
```
```jsx
const { createApp, ref } = Vue

const app = createApp({
  setup() {
    const imageSrc = ref('https://picsum.photos/200/')
    const myUrl = ref('https://www.google.co.kr/')
    const dynamicattr = ref('title')
    const dynamicValue = ref("Hello Vue.js")
    return {
      imageSrc,
      myUrl,
      dynamicattr,
      dynamicValue,
    }
  }
})
```

<br>

## Class and Style Bindings

- 클래스와 스타일은 모두 속성이므로 v-bind를 사용하여 다른 속성과 마찬가지로 동적으로 문자열 값을 할당할 수 있음
- 그러나 단순히 문자열 연결을 사용하여 이러한 값을 생성하는 것은 번거롭고 오류가 발생하기 쉬움
- Vue는 클래스 및 스타일과 함께 v-bind를 사용할 때 객체 또는 배열을 활용한 개선 사항을 제공

### 1-1. Binding HTML Classes - Binding to Objects

- 객체를 :class에 전달하여 클래스를 동적으로 전환
    - 예시: isActive의 T/F에 의해 active 클래스의 존재가 결정됨
        ```jsx
        const isActive = ref(false)
        ```
        ```html
        <div :class="{ active: isActive }">Text</div>
        ```
        
- 객체에 더 많은 필드를 포함하여 여러 클래스를 전환할 수 있음
    - 예시: `:class` directive를 일반 클래스 속성과 함께 사용 가능
        ```jsx
        const isActive = ref(false)
        const hasInfo = ref(true)
        ```
        ```html
        <div class="static" :class="{ active: isActive, 'text-primary': hasInfo}">Text</div>
        ```
        
        - `class`와 `:class` 따로 써도 알아서 하나로 합쳐짐
- 반드시 inline 방식으로 작성하지 않아도 됨
    - 예시
        ```jsx
        const isActive = ref(false)
        const hasInfo = ref(true)
        
        // ref는 반응 객체의 속성으로 액세스되거나 변경될 때 자동으로 unwrap
        const classObj = ref({
          active: isActive,
          'text-primary': hasInfo,
        })
        ```
        ```html
        <div class="static" :class="classObj">Text</div>
        ```
        

### 1-2. Binding HTML Classes - Binding to Arrays

- `:class`를 배열에 바인딩하여 클래스 목록을 적용할 수 있음
    - 예시
        ```jsx
        const activeClass = ref('active')
        const infoClass = ref('text-primary')
        ```
        ```html
        <div :class="[activeClass, infoClass]">Text</div>
        ```
        
- 배열 구문 내에서 객체 구문 사용
    - 예시
        ```html
        <div :class="[{ active: isActive }, infoClass]">Text</div>
        ```
        

### 2-1. Blinding Inline Styles - Binding to Objects

- `:style`은 JS객체에 대한 바인딩을 지원 (HTML style 속성에 해당)
    - 예시
        ```jsx
        const activeColor = ref('crimson')
        const fontSize = ref(50)
        ```

        ```html
        <div :style="{ color: activeColor, fontSize: fontSize + 'px' }">Text</div>
        ```
        
- 실제 CSS에서 사용하는 것처럼 `:style`은 kebab-cased 키 문자열도 지원 (단, camelCase 작성을 권장)
    - 예시
        ```html
        <div :style="{ 'font-size': fontSize + 'px'}">Text</div>
        ```
        
- 템플릿을 더 깔끔하게 작성하려면 스타일 객체에 직접 바인딩 하는 것을 권장
    - 예시
        ```jsx
        const styleObj = ref({
          color: activeColor,
          fontSize: fontSize.value + 'px'
        })
        ```
        ```html
        <div :style="styleObj">Text</div>
        ```
        
        - 반응형 변수에 반응형 변수가 들어갈 때는 auto unwrap이 된다
        - 하지만 반응형변수+문자열을 붙일 때는 `.value` 필수!

### 2-2. Blinding Inline Styles - Binding to Arrays

- 여러 스타일 객체의 배열에 `:style`을 바인딩할 수 있음
- 작성한 객체는 병합되어 동일한 요소에 적용
    - 예시
        ```jsx
        const styleObj2 = ref({
          color: 'blue',
          border: '1px solid black'
        })
        ```
        
        ```html
        <div :style="[styleObj, styleObj2]">Text</div>
        ```