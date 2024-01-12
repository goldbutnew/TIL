# Composition vs Inheritance

### Composition

- 합성
- 여러 개의 컴포넌트를 합쳐서 새로운 컴포넌트를 만드는 것
- 여러 개의 컴포넌트들을 어떻게 조합할지 고민해 봐야 함

### Composition의 종류

1. Containment
    - 하위 컴포넌트를 포함하는 형태의 합성 방법
    - sidebar나 dialog 같은 box 형태의 컴포넌트는 자신의 하위 컴포넌트를 미리 알 수 없다
    - 리액트의 props에 기본적으로 들어 있는 children이라는 속성을 사용해서 조합
    - 예제 코드: children prop을 사용한 FancyBorder
        
        ```jsx
        function FancyBorder(props) {
            return (
                <div className={'FancyBorder FancyBorder-' + props.color}>
                    {props.children}
                </div>
            )
        }
        ```
        
        - `props.children`을 사용하면 해당 컴포넌트의 하위 컴포넌트가 모두 children으로 들어오게 됨
        - React.createElement의 세 번째로 들어가는 파라미터가 children이었음!
        - children이 배열로 들어가는 이유: 여러 개의 하위 컴포넌트를 가질 수 있기 때문
        - Fancy border 컴포넌트는 하위 컴포넌트를 포함하여 예쁜 테두리로 감싸주는 컴포넌트가 됨!
        - 활용 예시
            
            ```jsx
            function WelcomeDialog(props) {
                return (
                    <FancyBorder color="blue">
                        <h1 className="Dialog-title">
                            어서오세요
                        </h1>
                        <p className="Dialog-message">
                            우리 사이트에 방문하신 것을 환영합니다!
                        </p>
                    </FancyBorder>
                )
            }
            ```
            

1. Specialization 
    - 전문화, 특수화
    - WelcomeDialog는 Dialog의 특별한 케이스 → dialog는 범용적인 개념이지만 welcomedialog는 누군가를 반기기 위한 dialog
    - 범용적인 개념을 구별이 되도록 구체화하는 것
    - 기존의 객체지향 언어에서는 상속을 사용하여 specialization을 구현
    - 하지만 리액트에서는 합성을 사용!
    - 예제 코드
        
        ```jsx
        function Dialog(props) {
          return (
            <FancyBorder color="blue">
              <h1 className="Dialog-title">
                {props.title}
              </h1>
              <p className="Dialog-message">
                {props.message}
              </p>
            </FancyBorder>
          );
        }
        
        function WelcomeDialog() {
          return (
            <Dialog
              title="Welcome"
              message="Thank you for visiting our spacecraft!" />
          );
        }
        ```
        
        - dialog의 title과 message에 따라 welcome dialog가 될 수도 있고, warning dialog가 될 수도 있음

### Containment와 Specialization 같이 사용하기

```jsx
function Dialog(props) {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        {props.title}
      </h1>
      <p className="Dialog-message">
        {props.message}
      </p>
      {props.children}
    </FancyBorder>
  );
}
```

```jsx
import { useState } from "react";

function SignUpDialog(props) {
    const [nickname, setNickname] = useState('')

    const handleChange = (event) => {
        setNickname(event.target.value)
    }

    const handleSignUp = () => {
        alert(`어서 오세요, ${nickname}님!`)
    }
    
    return (
        <Dialog
            title="화성 탐사 프로그램"
            message="닉네임을 입력해 주세요.">
            <input
                value={nickname}
                onChange={handleChange}
            />
            <button onClick={handleSignUp}>
                가입하기
            </button>
        </Dialog>
    )
}
```

### Inheritance

- 상속
- 부모 클래스를 상속받아서 새로운 자식 클래스를 만든다는 것 → 자식 클래스가 부모 클래스의 모든 속성을 가짐
- 하지만 리액트는 상속보다 합성을 권장
- 복잡한 컴포넌트를 쪼개서 여러 개의 컴포넌트를 만들고 만든 컴포넌트들을 조합해서 새로운 컴포넌트를 만들자