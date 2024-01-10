# Handling Events

### Event

- 이벤트
- 특정 사건 (ex. 사용자가 버튼을 클릭한 사건)
- 이벤트 핸들링? 이벤트를 처리하는 것

### DOM Event

```jsx
<button onclick="activate()">
    Activate
</button>
```

### React Event

```jsx
<button onClick={activate}>
    Activate
</button>
```

- 이벤트 이름 표기법: 리액트에선 Camel case로
- 함수 전달 방식: DOM에서는 이벤트 처리할 함수를 문자열로 전달하지만, 리액트에서는 함수 그대로 사용

### Event Handler

- 어떤 사건이 발생하면 사건을 처리하는 역할

### Event Listener

- 이벤트 Handler을 다른 이름
- 이벤트가 발생하는 것을 계속 듣고 있다는 의미

### 예제 코드

```jsx
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // 콜백에서 `this`가 작동하려면 아래와 같이 바인딩 해주어야 합니다.
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(prevState => ({
      isToggleOn: !prevState.isToggleOn
    }));
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}
```

- bind 하는 이유: 자바스크립트에서는 기본적으로 클래스 함수들이 바운드 되지 않음
- bind 형식이 번거롭게 느껴진다면? Class fields syntax 사용
    
    ```jsx
    class LoggingButton extends React.Component {
      // 이 문법은 `this`가 handleClick 내에서 바인딩되도록 합니다.
      // 주의: 이 문법은 *실험적인* 문법입니다.
      handleClick = () => {
        console.log('this is:', this);
      };
    
      render() {
        return (
          <button onClick={this.handleClick}>
            Click me
          </button>
        );
      }
    }
    ```
    
- 둘 다 싫으면? 콜백에 화살표 함수(Arrow function) 사용
    
    ```jsx
    class LoggingButton extends React.Component {
      handleClick() {
        console.log('this is:', this);
      }
    
      render() {
        // 이 문법은 `this`가 handleClick 내에서 바인딩되도록 합니다.
        return (
          <button onClick={() => this.handleClick()}>
            Click me
          </button>
        );
      }
    }
    ```
    
    - 다만 이 방식은 마이 버튼 컴포넌트가 렌더링 될 때마다 다른 콜백함수가 생성되는 문제가 있음
    - 이 콜백 함수가 하위 컴포넌트의 props으로 넘겨지게 되면 하위 컴포넌트에서 추가적인 렌더링 발생
- 하지만 함수 컴포넌트는 이제 거의 사용하지 않기 때문에 대충 이해하고 넘기셈

### 함수 컴포넌트의 이벤트 처리 방법

```jsx
function Toggle(props) {
    const [isToggleOn, setIsToggleOn] = useState(true)

    // 방법 1. 함수 안에 함수로 정의
    function handleClick() {
        setIsToggleOn((isToggleOn) => !isToggleOn)
    }

    // 방법 2. arrow function을 사용하여 정의
    const handleClick = () => {
        setIsToggleOn((isToggleOn) => !isToggleOn)
    }

    // this 사용하지 않고 onClick에 곧바로 정의한 이벤트 핸들러 넣어 주면 됨
    return (
        <button onClick={handleClick}>
            {isToggleOn ? "켜짐": "꺼짐"}
        </button>
    )
}
```

### Argument 전달하기

- Argument
    - 프로그래밍에서는 ‘함수에 주장할 내용’ 정도의 의미
    - 함수(이벤트 핸들러)에 전달할 데이터
- Parameter
    - 매개변수
- 예제코드 (1)
    
    ```jsx
    //arrow function
    <button onClick={(event) => this.deleteItem(id, event)}>삭제하기</button>
    
    // bind
    <button onClick={this.deleteItem.bind(this, id)}>삭제하기</button>
    ```
    
    - 둘 다 첫 번째 매개변수는 id, 두 번째는 이벤트가 전달됨
        - 첫 번째는 명시적으로 event를 넣어 주었고
        - 두 번째는 id 이후에 두 번째 매개변수로 자동 들어감
- 예제코드 (2)
    
    ```jsx
    function Mybutton(props) {
        const handleDelete = (id, event) => {
            console.log(id, event.target)
        }
    
        return (
            <button onClick={(event) => handleDelete(1, event)}>
                삭제하기
            </button>
        )
    }
    ```
    
    - 1
        
        ```jsx
        import React from "react"
        
        class ConfirmButton extends React.Component {
            constructor(props) {
                super(props)
                
                this.state = {
                    isConfirmed: false,
                }
        
                this.handleConfirm = this.handleConfirm.bind(this)
            }
        
            handleConfirm() {
                this.setState((prevState) => ({
                    isConfirmed: !prevState.isConfirmed
                }))
            }
        
            render() {
                return (
                    <button
                        onClick={this.handleConfirm}
                        disabled={this.state.isConfirmed}
                    >
                        {this.state.isConfirmed ? "확인됨": "확인하기"}
                    </button>
                )
            }
        }
        
        export default ConfirmButton
        ```
        
    - 화살표 함수로 수정
        
        ```jsx
        import React from "react"
        
        class ConfirmButton extends React.Component {
            constructor(props) {
                super(props)
                
                this.state = {
                    isConfirmed: false,
                } 
            }
        
            handleConfirm = () => {
                this.setState((prevState) => ({
                    isConfirmed: !prevState.isConfirmed
                }))
            }
        
            render() {
                return (
                    <button
                        onClick={this.handleConfirm}
                        disabled={this.state.isConfirmed}
                    >
                        {this.state.isConfirmed ? "확인됨": "확인하기"}
                    </button>
                )
            }
        }
        
        export default ConfirmButton
        ```
        
    - 함수 컴포넌트
        
        ```jsx
        import react, { useState } from "react"
        
        function ConfirmButton(props) {
            const [isConfirmed, setIsConfirmed] = useState(false)
        
            const handleConfirm = () => {
                setIsConfirmed((prevIsConfirmed) => !prevIsConfirmed)
            }
        
            return (
                <button onClick={handleConfirm} disabled={isConfirmed}>
                    {isConfirmed ? "확인됨": "확인하기"}
                </button>
            )
        }
        
        export default ConfirmButton
        ```