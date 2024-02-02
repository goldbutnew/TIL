# Lifecycle Hooks
- Vue 인스턴스의 생애주기 동안 특정 시점에 실행되는 함수
- 개발자가 특정 단계에서 의도하는 로직이 실행될 수 있도록 함

### Lifecycle Hooks 예시
1. Vue 컴포넌트 인스턴스가 초기 렌더링 및 DOM 요소 생성이 완료된 후 특정 로직을 수행하기 
    ```jsx
    const { createApp, ref, onMounted} = Vue
    ```
    ```jsx
    onMounted(() => {
      console.log('mounted')
    })
    ```
    
2. 반응형 데이터의 변경으로 인해 DOM이 업데이트 된 후 특정 로직을 수행하기  
    ```html
    <div id="app">
      <button @click="count++">Add 1</button>
      <p>Count: {{ count }}</p>
      <p>{{ message }}</p>
    </div>
    ```
    ```jsx
    const count = ref(0)
    const message = ref(null)
    
    onUpdated(() => {
      message.value = 'updated!'
    })
    ```
3. 반응형 데이터의 변경으로 인해 컴포넌트의 DOM이 업데이트 된 후 특정 로직을 수행
    ![Untitled](https://github.com/goldbutnew/TIL/assets/149566915/96743f1a-822b-4a28-962a-8e06c7021398)

    

### Lifecycle Hooks 특징
- Vue는 Lifecycle Hooks에 등록된 콜백 함수들을 인스턴스와 자동으로 연결
- 이렇게 동작하려면 hooks 함수들은 반드시 동기적으로 작성되어야 함
- 인스턴스 생애 주기의 여러 단계에서 호출되는 다른 hooks도 있으며. 가장 일반적으로 사용되는 것은 `onMounted`, `onUpdated`, `onUnmounted`