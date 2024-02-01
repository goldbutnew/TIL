# Watchers

### watch()
- 반응형 데이터를 감시하고, 감시하는 데이터가 변경되면 콜백 함수 호출

### watch 구조
```jsx
watch(variable, (newValue, oldValue) => {
	// do something
}
```
- `variable`: 감시하는 변수
- `newValue`: 콜백 함수의 첫 번째 값(감시하는 변수가 변화된 값)
- `oldValue`: 콜백 함수의 두 번째 인자

### watch 예시

1. 감시하는 변수에 변화가 생겼을 때 기본 동작 확인하기
    ```html
    <button @click="count++">Add 1</button>
    <p>Count: {{ count }}</p>
    ```
    ```jsx
    const count = ref(0)
    
    const countWatch = watch(count, (newValue, oldValue) => {
      console.log(`newValue: ${newValue}, oldValue: ${oldValue}`)
    })
    ```
    ![Untitled](https://github.com/goldbutnew/TIL/assets/149566915/5b76e9a8-5c64-4a8d-9e0c-9b7860d25d6c)

    
2. 감시하는 변수에 변화가 생겼을 때 연관 데이터 업데이트 하기
    
    ```html
    <input v-model="message">
    <p>Message length: {{ messageLength }}</p>
    ```
    ```jsx
    const message = ref('')
    const messageLength = ref(0)
    
    const messageWatch = watch(message, (newValue, oldValue) => {
      messageLength.value = newValue.length
    })
    ```
    ![Untitled 1](https://github.com/goldbutnew/TIL/assets/149566915/c0fa3598-7eeb-4fe8-8952-bd1886325e18)
    

### Computed와 Watchers
![Untitled 2](https://github.com/goldbutnew/TIL/assets/149566915/d91161f7-4bbd-411f-af44-1069101d5a0f)
- **computed와 watch 모두 의존(감시)하는 원본 데이터를 직접 변경하지 않음**