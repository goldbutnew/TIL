## v-if
### v-if
- 표현식 값의 T/F를 기반으로 요소를 조건부로 렌더링

### v-if 예시
- `v-else` directive를 사용하여 `v-if`에 대한 `else` 블록을 나타낼 수 있음
- if else
    ![Untitled](https://github.com/goldbutnew/TIL/assets/149566915/ec35b725-87b2-4648-890e-b343d802bbcc)
    ```jsx
    const isSeen = ref(true)
    ```
    ```html
    <p v-if="isSeen">true일때 보여요</p>
    <p v-else>false일때 보여요</p>
    <button @click="isSeen = !isSeen">토글</button>
    ```
- else if
    ```jsx
    const name = ref('Cathy')
    ```
    ```html
    <div v-if="name === 'Alice'">Alice입니다</div>
    <div v-else-if="name === 'Bella'">Bella입니다</div>
    <div v-else-if="name === 'Cathy'">Cathy입니다</div>
    <div v-else>아무도 아닙니다.</div>
    ```
    
### 여러 요소에 대한 v-if 적용
```jsx
<template v-if="name === 'Cathy'">
  <div>Cathy입니다</div>
  <div>나이는 30살입니다</div>
</template>
```
- v-if는 directive이기 때문에 단일 요소에만 연결 가능
- 이 경우 **template** 요소에 v-if를 사용하여 하나 이상의 요소에 대해 적용할 수 있음 (v-else, v-else-if 모두 적용 가능)

### HTML template element
- 페이지가 로드될 때 렌더링 되지 않지만 JS를 사용하여 나중에 문서에서 사용할 수 있도록 하는 HTML을 보유하기 위한 메커니즘
- 보이지 않은 wrapper 역할

<br>

## v-if vs. v-show

### v-show
- 표현식 값의 T/F를 기반으로 요소의 가시성(visibility)을 전환

### v-show 예시
```jsx
const isShow = ref(false)
```
```html
<div v-show="isShow">v-show</div>
```
![Untitled 1](https://github.com/goldbutnew/TIL/assets/149566915/155fbf4d-94d8-4ab8-ac63-641a16470f75)
- v-show 요소는 항상 렌더링 되어 DOM에 남아 있음
- CSS display 속성만 전환하기 때문

### v-if vs. v-show
- `v-if` (Cheap initial load, expensive toggle)
    - 초기 조건이 false인 경우 아무 작업도 수행하지 않음
    - 토글 비용이 높음
- `v-show` (Expensive inital load, cheap toggle)
    - 초기 조건에 관계 없이 항상 렌더링
    - 초기 렌더링 비용이 더 높음