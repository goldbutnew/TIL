# Rendering Element

### Element란?

- 리액트 앱을 구성하는 요소
- Element are the smallest building blocks of react apps
- 화면에 나타나는 내용을 기술하는 자바스크립트 객체

### React Element

- React Element는 DOM Element의 가상 표현
    
    ![Untitled](https://github.com/goldbutnew/TIL/assets/149566915/d2e65390-edf6-4037-aec0-43be64c53f1e)
    
- React Elements는 자바스크립트 객체 형태로 존재
- 마음대로 변경할 수 없는 불변성을 가지고 있음

### CreateElement

```jsx
React.createElement(
	type,
	[props],
	[...children]
)
```

### Element의 특징

- im + mutable = immutable
- 변하지 않는 성질
- 한 번 생성된 element는 변하지 않음
- element는 생성 후에 자식이나 속성 변경 불가
- component는 element로 이루어져 있고, element는 변경 불가함 (붕어빵과 붕어빵 속의 관계??)

### Element Rendering

- Root DOM Node
    
    ```jsx
    <div id="root"></div>
    ```
    
    - 모든 웹사이트는 단 하나의 루트 돔 노드를 가짐
    - 그러나 하나의 웹 사이트에 추가적으로 리액트를 연동하게 되면 여러 개의 분리된 수많은 루트 돔을 가질 수도 있음
- 활용 예시
    
    ```jsx
    const element = <h1>안녕, 리액트!</h1>
    ReactDOM.render(element, document.geElementById('root'))
    ```
    
    - `render`: 첫 번째 파라미터를 두 번째 파라미터에 렌더링 하는 함수
    - 리액트 엘리먼트가 렌더링 되는 과정은 버추얼 돔에서 실제 돔으로 이동하는 과정

### 렌더링 된 Element Update 하기

- 불변성 때문에 업데이트 하기 위해서는 다시 생성해야 함
- 예시
    
    ```jsx
    function tick() {
      const element = (
        <div>
          <h1>안녕, 리액트!</h1>
          <h2>현재 시간: {new Date().toLocaleTimeString()}</h2>
        </div>
      )
    
      ReactDOM.render(element, document.getElementById('root'))
    
    setInterval(tick, 1000)
    ```