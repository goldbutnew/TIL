# Vue Router

## 개요

### Vue Router

- Vue 공식 라우터 (The official Router for Vue.js)

### Vue Router 추가

1. Vite 프로젝트 생성 시 Router 추가
    
    ```bash
    $ npm create vue@latest
    
    Vue.js - The Progressive JavaScript Framework
    
    √ Project name: ... vue-project
    √ Add TypeScript? ... No / Yes
    √ Add JSX Support? ... No / Yes
    √ Add Vue Router for Single Page Application development? ... No / **Yes**
    √ Add Pinia for state management? ... No / Yes
    √ Add Vitest for Unit Testing? ... No / Yes
    √ Add an End-to-End Testing Solution? » No
    √ Add ESLint for code quality? ... No / Yes
    ```
    
2. 서버 실행 후 Router로 인한 프로젝트 변화 확인
    - Home, About 링크에 따라 변경되는 URL과 새로 렌더링 되는 화면

### Vue 프로젝트 구조 변화

1. App.vue 코드 변화
    ```html
    <template>
      <header>
        <nav>
          <RouterLink to="/">Home</RouterLink>
          <RouterLink to="/about">About</RouterLink>
        </nav>
      </header>
    
      <RouterView />
    </template>
    ```
    
    - RouterLink
        - 페이지를 다시 로드하지 않고 URL을 변경하고 URL 생성 및 관련 로직을 처리
        - HTML의 a 태그를 렌더링
    - RouterView
        - URL에 해당하는 컴포넌트를 표시
        - 어디에나 배치하여 레이아웃에 맞출 수 있음
2. router 폴더 생성
    - router/index.js
        - 라우팅에 관련된 정보 및 설정이 작성되는 곳
        - router URL과 컴포넌트를 매핑
3. views 폴더 생성
    - views
        - RouterView 위치에 렌더링 할 컴포넌트를 배치
        - 기존 components 폴더와 기능적으로 다른 것은 없으며 단순 분류의 의미로 구성됨
        - **일반 컴포넌트와 구분하기 위해 컴포넌트 이름을 View로 끝나도록 작성하는 것을 권장**

# Basic Routing

## 라우팅 기본

1. `index.js`에 라우터 관련 설정 작성(주소, 이름, 컴포넌트)
2. RouterLink의 `to` 속성으로 `index.js`에서 정의한 주소 속성값(path)을 사용

## Named Routes

- 경로에 이름을 지정하는 라우팅

### Named Routes 예시

- name 속성값에 경로에 대한 이름을 지정
- 경로에 연결하려면 RouterLink에 v-bind를 사용해 `to` prop 객체로 전달

```jsx
// src/router/index.js

const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes: [
    {
      path: '/',
      name: 'home',
      component: HomeView
    },
    ...
  ]
})
```

```html
<!-- App.vue -->

<RouterLink to="/">Home</RouterLink>
<RouterLink to="/about">About</RouterLink>
```

### Named Routes 장점

- 하드 코딩된 URL을 사용하지 않아도 됨
- URL 입력 시 오타 방지

## Dynamic Route Matching with Params

### 매개 변수를 사용한 동적 경로 매칭

- 주어진 패턴 경로를 동일한 컴포넌트에 매핑해야 하는 경우 활용
- 예를 들어 모든 사용자의 ID를 활용하여 프로필 페이지 url을 설계한다면?
    - user/1
    - user/2
    - 일정한 패턴의 URL 작성을 반복해야 함

### 매개 변수를 사용한 동적 경로 매칭 활용

1. UserView 컴포넌트 작성’
    
    ```html
    <!-- UserView.vue -->
    
    <template>
      <div>
        <h1>UserView</h1>
      </div>
    </template>
    ```
    
2. UserView 컴포넌트 라우트 등록
    
    ```jsx
    // index.js
    
    import UserView from '../views/UserView.vue'
    
    const router = createRouter({
      routes: [
        {
          path: '/user/:id',
          name: 'user',
          component: UserView,
        },
    	]
    })
    ```
    
    - 매개변수는 콜론(:)으로 표기
3. 라우트의 매개변수는 컴포넌트에서 `$route.params`로 참조 가능
    
    ```html
    <!-- UserView.vue -->
    
    <template>
      <div>
        <h1>UserView</h1>
        <h2>{{ $route.params.id }}번의 User 페이지</h2>
      </div>
    </template>
    ```
    
4. 다만 다음과 같이 Composition API 방식으로 작성하는 것을 권장
    
    ```html
    <!-- UserView.vue -->
    
    <template>
      <div>
        <h1>UserView</h1>
        <h2>{{ userId }}번의 User 페이지</h2>
      </div>
    </template>
    
    <script>
      import { ref } from 'vue'
      import { useRoute } from 'vue-router';

      const route = useRoute()
      const userId  = ref(route.params.id)
    </script>
    ```

## Programmatic Navigation

### 프로그래밍 방식 네비게이션

- router의 인스턴스 메서드를 사용해 RouterLink로 a 태그를 만드는 것처럼 프로그래밍으로 네비게이션 관련 작업을 수행할 수 있음
    - 다른 위치로 이동하기: `router.push()`
    - 현재 위치 바꾸기: `router.replace()`

### router.push()

- Navigate to a different location
- 다른 URL로 이동하는 메서드
- 새 항목을 history stack에 push 하므로 사용자가 브라우저 뒤로 가기 버튼을 클릭하면 이전 URL로 이동할 수 있음
- RouterLink를 클릭했을 때 내부적으로 호출되는 메서드 → RouterLink를 클릭하는 것은 router.push()를 호출하는 것과 같음

---

- 활용: UserView 컴포넌트에서 HomeView 컴포넌트로 이동하는 버튼 만들기
    
    ```html
    <!-- UserView.vue -->
    
    <script>
      import { useRoute, useRouter } from 'vue-router';

      const router = useRouter()

      const goHome = function () {
        router.push({ name: 'home' })
      }
    </script>
    ```
    
    ```html
    <!-- UserView.vue -->
    
    <button @click="goHome">홈으로!</button>
    ```

### router.replace()

- Reokace current location
- push 메서드와 달리 histroy stack에 새로운 항목을 push 하지 않고 다른 URL로 이동 (=== 이동 전 URL로 뒤로 가기 불가)