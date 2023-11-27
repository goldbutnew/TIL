# Introduction of Vue

## Front-end Development

### Client-side frameworks

#### Front-end Development

- 웹사이트와 웹 애플리케이션의 사용자 인터페이스(UI)와 사용자 경험(UX)을 만들고 디자인하는 것
- HTML, CSS, JS 등을 활용하여 사용자가 직접 상호작용하는 부분을 개발

#### Client-side frameworks

- 클라이언트 측에서 UI와 상호작용을 개발하기 위해 사용되는 JS 기반 프레임워크
- 예시:
    
    ![Untitled](https://github.com/goldbutnew/TIL/assets/149566915/d8cba892-1fd7-4f6a-a9b6-72849df41c45)
    

#### Client-side frameworks가 필요한 이유

- 웹에서 하는 일이 많아졌다
    1. 단순히 무언가를 읽는 곳 → 하는 곳
        1. 문서를 읽을 뿐 아니라 음악 스트리밍, 영화 감상 실시ㅣ
        2. 이와 같은 현대적이고 복잡한 대화형 웹사이트 → **웹 애플리케이션**
    2. 다루는 데이터가 많아졌다
        1. 애플리케이션의 기본 데이터를 안정적으로 추적하고 업데이트하는 도구 필요
        2. 애플리케이션의 상태를 변경할 때마다 일치하도록 UI 업데이트해야 함

### SPA

#### Single Page Application (SPA)

- 페이지 한 개로 구성된 웹 애플리케이션
- 웹 애플리케이션의 초기 로딩 후 새로운 페이지 요청 없이 동적으로 화면을 갱신하며 사용자와 상호작용하는 웹 애플리케이션 → CSR 방식

#### Client-side Rendering (CSR)

- 클라이언트에서 화면을 렌더링하는 방식
    1. 브우저는 페이지에 필요한 최소한의 HTML 페이지와 JS를 다운로드
    2. 그런 다음 JS를 사용하여 DOM을 업데이트 하고 페이지를 렌더링

---

- CSR 장점
    - 빠른 속도
    - 사용자 경험
    - Front-end와 Back-end의 명확한 분리

- CSR 단점
    - 초기 구동속도가 느림
    - SEO(검색 엔진 최적화) 문제

## Vue

- Vue CDN
    
    ```jsx
    <script src="[https://unpkg.com/vue@3/dist/vue.global.js](https://unpkg.com/vue@3/dist/vue.global.js)"></script>
    ```
    

### What is vue

- 사용자 인터페이스를 구축하기 위한 JS 프레임워크

---

- Vue를 학습하는 이유
    - 쉬운 학습 곡선 및 간편한 문법
    - 반응성 시스템
    - 모듈화 및 유연한 구조

#### Vue의 2가지 핵심 기능

1. 선언적 렌더링 (Declarative Rendering)
    - HTML을 확장하는 템플릿 구문을 사용하여 HTML이 JS 데이터를 기반으로 어떻게 보이는지 설명할 수 있음
2. 반응형 (Reactivity)
    - JS 상태 변경사항을 자동으로 추적하고 변경사항이 발생할 때 DOM을 효율적으로 업데이트

---

- 예시
    
    ```html
    <div id="app">
      <h1>{{ greeting }}</h1>
      <button @click="count++">{{ count }}</button>
    </div>
    ```
    
    ```jsx
    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
    <script>
      // JS 구조 분해 할당
      const { createApp, ref } = Vue
    
      const app = createApp({
        setup () {
          const count = ref(0)
          const greeting = ref('Hello!')
          return {
            count,
            greeting
          }
        }
      })
    
      app.mount('#app')
    </script>
    ```
    

### Vue Tutorial

#### Vue를 사용하는 방법

1. CDN 방식
2. NPM 설치 방식 → CDN 방식 이후 진행

#### 첫 번째 Vue 작성하기

1. CDN 및 Application instance 작성
    
    ```jsx
    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
    <script>
      const { createApp } = Vue
    
      const app = createApp({
    </script>
    ```
    
2. Application instance
    - 모든 Vue 애플리케이션은 createApp 함수로 새 Application instance를 생성하는 것으로 시작
    - 외워야 할 것: 앱을 생성하는 이름 createapp이고
    
    ```jsx
    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
    <script>
      const { createApp } = Vue
    
      const app = createApp({})
    
      app.mount('#app')
    </script>
    ```
    
3. `app.mount()`
    - 컨테이너 요소에 애플리케이션 인스턴스를 탑재(연결)
    - 각 앱 인스턴스에 대해 `mount()` 는 한 번만 호출할 수 있음
    
    ```jsx
    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
    <script>
      const { createApp } = Vue
    
      const app = createApp({})
    
      app.mount('#app')
    </script>
    ```
    

#### ref()

- 반응형 상태(데이터)를 선언하는 함수(Declaring Reactive State)
- 반응형을 가지는 참조 변수를 만드는 것
- ref === reactive reference

#### ref 함수

- 인자를 받아 `.value` 속성이 있는 ref 객체로 래핑(wrapping) 하여 반환
- ref로 선언된 변수의 값이 변경되면, 해당값을 사용하는 탬플릿에서 자동으로 업데이트
- 인자는 어떠한 타입도 가능

```jsx
const { createApp, **ref** } = Vue

const app = createApp({
  setup() {
    const message = ref('Hello Vue!')
    console.log(message) // ref 객체
    console.log(message.value) // Hello Vue!
  }
})
```

---

- 탬플릿의 참조에 접근하려면 setup 함수에서 선언 및 반환 필요
- 탬플릿에서 `ref`를 사용할 때는 `.value`를 작성할 필요 없음 (자동으로 unwrapped)

```html
<div id="app">
  <h1>{{ message }}</h1>
</div>
```

```jsx
const app = createApp({
  setup() {
    const message = ref('Hello Vue!')
    return {
      message
    }
  }
})
```

#### Vue 기본 구조

- `createApp()`에 전달되는 객체는 Vue 컴포넌트(Component)
- 컴포넌트의 상태는 `setup()` 함수 내에서 선언되어야 하며 **객체를 반환해야 함**

```jsx
const app = createApp({
  setup() {
    const message = ref('Hello Vue!')
    return {
      message
    }
  }
})
```

#### 템플릿 렌더링

- 반환된 객체의 속성은 템플릿에서 사용할 수 있음
- Mustache syntax(콧수염 구문)를 사용하여 메시지 값을 기반으로 동적 텍스트를 렌더링
    
    ```html
    <h1>{{ message }}</h1>
    ```
    
    ```jsx
    <div id="app">
      <h1>**{{ message }}**</h1>
    </div>
    ```
    
    - 결과물:
        
        ![Untitled 1](https://github.com/goldbutnew/TIL/assets/149566915/80335714-f965-4557-a031-10029216b8c8)
        
- 콘텐츠는 식별자나 경로에만 국한되지 않으며 유효한 JS 표현식을 사용할 수 있음
    
    ```html
    <h1>{{ message.split('').reverse().join('') }}</h1>
    ```
    
    - 결과물:

        ![Untitled 2](https://github.com/goldbutnew/TIL/assets/149566915/32d61f0b-74fd-49d6-a10b-daeaac2c456b)
        

#### Event Listeners in Vue

- `v-on` directive를 사용하여 DOM 이벤트를 수신할 수 있음
    - 자세한 directive 학습은 다음 시간에 진행
- 함수 내에서 refs를 변경하여 구성 요소 상태를 업데이트

```html
<div id="app">
  <button v-on:click="increment">{{ count }}</button>
</div>
```

```jsx
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const { createApp, ref } = Vue

  const app = createApp({
    setup() {
      const count = ref(0)
      const increment = function () {
        count.value++
      }
      return {
        count,
        increment
      }
    }
  })

  app.mount('#app')
</script>
```

## 참고

### Ref Unwrap 주의사항

#### 탬플릿에서의 unwrap 시 주의사항

- 탬플릿에서의 unwrap은 ref가 최상위 속성인 경우에만 적용 가능

---

- 다음 표현식은 어떻게 출력될까?
    
    ```jsx
    const object = { id: ref(0) }
    ```
    
    ```html
    {{ object.id + 1 }}
    ```
    
- 이 문제를 해결하기 위해서는 id를 최상위 속성으로 분해해야 함
    
    ```html
    const { id } = object
    ```
    
    ```jsx
    {{ id + 1 }}
    ```
    
- 단, ref가 `{{ }}`의 최종 평가값인 경우에는 unwrap 사용
    
    ```jsx
    {{ object.id }} // == {{ object.id.value }}
    ```
    

#### Why Refs?

- 일반 변수 대신 굳이 `.value` 가 포함된 ref가 필요한 이유는?
    - 의존성 추적 기반의 반응형 시스템
    - Vue는 렌더링 중에 사용된 모든 ref를 추적하며 나중에 ref가 변경되면 이를 추적하는 구성 요소에 대해 다시 렌더링
    - JS에서는 일반 변수의 접근 또는 변형을 감지할 방법이 없다!

#### SEO

- Search Engine Optimization
- 검색 엔진에서 내 서비스나 제품 등이 효율적으로 검색 엔진에 노출되도록 개선하는 과정을 일컫는 작업

#### CSR & SSR

- CSR과 SSR은 흑백이 아님!