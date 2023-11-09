# Navigation Guard

## 개요

### Navigation Guard

- Vue router를 통해 특정 URL에 접근할 때 다른 URL로 redirect를 하거나 취소하여 네비게이션을 보호
- ex) 인증 정보가 없으면 특정 페이지에 접근하지 못하게 함

### Navigation Guard의 종류

1. Globally (전역 가드)
    - 애플리케이션 전역에서 동작
    - index.js에서 정의
2. Per-route (라우터 가드)
    - 특정 route에서만 동작
    - index.js의 각 routes에 정의
3. In-component (컴포넌트 가드)
    - 특정 컴포넌트 내에서만 동작
    - 컴포넌트 Script에 정의

## Globally Guard

### router.beforeEach()

- 다른 URL로 이동하기 직전에 실행되는 함수
- Global Before Guards

### router.beforeEach 구조

```jsx
router.beforeEach((to, from) => {
	...
	return false
})
```

- `to`: 이동할 URL 정보가 담긴 Route 객체
- `from`: 현재 URL 정보가 담긴 Route 객체
- 선택적 반환(return)값:
    - false
        - 현재 내비게이션을 취소
        - 브라우저 URL이 변경된 경우(사용자가 수동으로 또는 뒤로 버튼을 통해) from 경로의 URL로 재설정
    - Route Location
        - `router.push()`를 호출하는 것처럼 경로 위치를 전달하여 다른 위치로 `redirect`
        - return이 없다면 `to` URL Route 객체로 이동

### router.beforeEach 예시

1. 전역가드 beforEach 작성
    
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
    
2. HomeView에서 UserView로 이동 후 각 인자의 값 출력 확인하기
    <img src="https://github.com/goldbutnew/TIL/assets/149566915/0a8cd409-71a2-46e7-9d74-c8679c0aa638">
    - `to`: 이동할 URL인 user 라우트에 대한 정보가 들어있음
    - `from`: 현재 URL인 home 라우트에 대한 정보가 들어있음

### router.beforeEach 활용

1. 사전 준비: LoginView 컴포넌트 작성 및 라우트 등록
    
    ```html
    <!-- LoginView -->
    
    <template>
      <div>
        <h1>Login View</h1>
      </div>
    </template>
    ```
    
    ```jsx
    // index.js
    
    {
      path: '/login',
      name: 'login',
      component: LoginView,
    },
    ```
    
    ```html
    <!-- App.vue -->
    
    <RouterLink :to="{ name: 'login' }">Login</RouterLink>
    ```
    
2. Login이 되어 있지 않다면 페이지 진입을 막고 Login 페이지로 이동시키기
    - 어떤 RouterLink를 클릭해도 LoginView 컴포넌트만 볼 수 있음
    - 만약 로그인되어 있지 않고(1), 이동하는 주소 이름이 login이 아니라면(2) login 페이지로 redirect
    
    ```jsx
    // index.js
    
    router.beforeEach((to, from) => {
      const isAuthenticated = false
      
      if (!isAuthenticated && to.name !== 'login') {
        console.log('로그인이 필요합니다.')
        return { name: 'login' }
      }
    })
    ```
    

## Per-route-Guard

### router.beforeEnter()

- route에 진입했을 때만 실행되는 함수
- 매개변수, 쿼리값이 변경될 때는 실행되지 않고 다른 경로에서 탐색할 때만 실행됨

### router.beforeEnter 구조

```jsx
{
  path: '/user/:id',
  name: 'user',
  component: UserView,
  beforeEnter: (to, from) => {
    ...
	return false
  }
},
```

- routes 객체에서 정의
- 함수의 `to`, `from`, 선택 반환 인자는 beforeEach와 동일

### router.beforeEnter 예시

1. 라우터 가드 beforeEnter 작성
    
    ```jsx
    {
      path: '/user/:id',
      name: 'user',
      component: UserView,
      beforeEnter: (to, from) => {
        console.log(to)
        console.log(from)
      }
    },
    ```
    
2. HomeView에서 Userview로 이동 후 각 인자 값 출력 확인하기
    - `to`: 이동할 URL인 user 라우트에 대한 정보가 들어있음
    - `from`: 현재 URL인 home 라우트에 대한 정보가 들어있음
    - 다른 경로에서 user 라우트를 탐색했을 때 실행된 것
    

### router.beforEnter 활용

1. 전역가드 작성 주석 처리하기
2. 이미 로그인 한 상태라면 LoginView 진입을 막고 HomeView로 이동시키기 
    
    ```jsx
    // index.js
    
    const isAuthenticated = true
    
    {
      path: '/login',
      name: 'login',
      component: LoginView,
      beforeEnter: (to, from) => {
        if (isAuthenticated === true) {
          console.log('이미 로그인되어 있습니다.')
          return { name: 'home' }
        }
      }
    },
    ```
    

## In-component Guard

### 컴포넌트 가드 종류

- onBeforeRouteLeave
    - 현재 라우트에서 다른 라우트로 이동하기 전에 실행
    - 사용자가 현재 페이지를 떠나는 동작에 대한 로직을 처리
- onBeforeRouteUpdate
    - 이미 렌더링된 컴포넌트가 같은 라우트 내에서 업데이트 되기 전에 실행
    - 라우트 업데이트 시 추가적인 로직을 처리

### onBeforeRouteLeave 활용

- 사용자가 UserView를 떠날 시 팝업 창 출력하기
    
    ```html
    <!-- UserView.vue -->
    
    <script>
    	import { onBeforRouteLeave } from 'vue-router'
    
      onBeforeRouteLeave((to, from) => {
        const answer = window.confirm('정말 떠나실 건가요?')
        if (answer === false) {
          return false
        }
      })
    </script>
    ```
    

### onBeforeRouteUpdate 활용

- UserView 페이지에서 다른 id를 가진 User의 UserView 페이지로 이동하기
    
    ```html
    <!-- UserView.vue -->
    
    <template>
      <div>
    		<!-- 100번의 User 페이지라고 정상 출력 -->
    		<h2>{{ $route.params.id }}번의 User 페이지</h2> 
    		<!-- userId 변화 없음 -->
        <h2>{{ userId }}번의 User 페이지</h2>
        <button @click="goAnotherUser">100번 유저 페이지로!</button>
      </div>
    </template>
    
    <script>
    	import { onBeforRouteLeave, onBeforeRouteUpdate } from 'vue-router'
    	
    	const userId  = ref(route.params.id)
    
    	// const로 선언한 userId가 업데이트 되지 않는 문제 발생
    	const goAnotherUser = function () {
        router.push({ name: 'user', params: {id: 100} })
      }
     
    	// 해결
      onBeforeRouteUpdate((to, from) => {
        userId.value = to.params.id
      })
    </script>
    ```
    
    - onBeforRouteUpdate에서 userId를 변경하지 않으면 userId는 갱신되지 않음
    - 컴포넌트가 재사용되었기 때문!