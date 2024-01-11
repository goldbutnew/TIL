# Conditional Rendering

### Conditional Redering이란?

- 조건에 따른 렌더링
- 조건부 렌더링
- 조건문의 결과에 따라 값이 true나 false가 나오는데 그 결과값에 따라 다르게 렌더링 하는 것

### 예제

1. 함수 컴포넌트 생성
    
    ```jsx
    function UserGreeting(props) {
      return <h1>Welcome back!</h1>;
    }
    
    function GuestGreeting(props) {
      return <h1>Please sign up.</h1>;
    }
    ```
    
2. 조건부 렌더링
    
    ```jsx
    function Greeting(props) {
      const isLoggedIn = props.isLoggedIn;
      if (isLoggedIn) {
        return <UserGreeting />;
      }
      return <GuestGreeting />;
    }
    
    const root = ReactDOM.createRoot(document.getElementById('root')); 
    // Try changing to isLoggedIn={true}:
    root.render(<Greeting isLoggedIn={false} />);
    ```
    

### JS의 Truthy와 Fasly

- 프로그래밍 언어에서 Boolean 자료형이 존재
- 하지만 JS는 참이라고 여겨지는 값과 거짓이라고 여겨지는 값이 존재
- Truthy: true는 아니지만 true라고 여겨지는 값
- Falsy: false는 아니지만 false라고 여겨지는 값
- 예시
    - Truthy
        - true
        - {} (empty object)
        - [] (empty array)
        - 42 (number, not zero)
        - “0”, “false” (string, not empty)
    - Falsy
        - false
        - 0, -0 (zero, minus zero)
        - 0n (BigInt zero)
        - ‘’, “”, `` (empty string)
        - null
        - undefined
        - NaN (not a number)

### Element Variables

- 엘리먼트 변수
- 리액트의 엘리먼트를 변수처럼 다루는 방법
- 예제 코드
    ```jsx
    function LoginControl(props) {
        const [isLoggedIn, seIsLoggedIn] = useState(false)
    
        const handleLoginClick = () => {
            setIsLoggedIn(true)
        }
    
        const handleLogoutClick = () => {
            setIsLoggedIn(fasle)
        }
        
        let button;
        if (isLoggedIn) {
        button = <LogoutButton onClick={this.handleLogoutClick} />;
        } else {
        button = <LoginButton onClick={this.handleLoginClick} />;
        }
    
        return (
            <div>
                <Greeting isLoggedIn={isLoggedIn} />
                {button}
            </div>
        );
    }
    ```
    - {button} ⇒ 컴포넌트라고 했지만 실제로는 컴포넌트로부터 생성된 리액트 엘리먼트

---

### Inline Conditions

- 코드를 별도로 분리된 곳에 작성하지 않고, 조건문을 코드 안에 집어 넣는 것

### Inline If

- if문을 필요한 곳에 직접 넣어 사용
- if문의 경우, 실제로 if문을 넣지 않고 `&&` 연산자를 사용해서 동일 효과
- 로지컬 and 연산
- 양쪽 조건이 모두 true인 경우에만 전체 결과 true
- `true && expression → expression`
- `false && expression → false` (두 번째 조건문은 평가하지 않음)
- 단축 평가 → 굳이 불필요한 연산은 하지 않도록 하기 위해서 사용
- 예제 코드
    ```jsx
    function Mailbox(props) {
      const unreadMessages = props.unreadMessages;
    
      return (
        <div>
          <h1>Hello!</h1>
          {unreadMessages.length > 0 &&
            <h2>
              You have {unreadMessages.length} unread messages.
            </h2>
          }
        </div>
      );
    }
    ```
    - `unreadMessages.length > 0`의 결과 값에 따라서 h2 태그로 둘러싸인 부분의 렌더링 결정
    - && 연산자 사용할 때 조건문 false이면 다음 표현식은 평가되지 않지만 표현식이 그대로 리턴됨

### Inline If-Else

- `if-else`문을 필요한 곳에 직접 넣어서 사용하는 방법
- 보여주거나 안 보여주는 두 가지 조건 뿐이던 Inline If와 달리, If-Else는 조건문의 값에 따라 다른 엘리먼트를 보여줄 때 사용
- `?` 연산자를 사용 → 삼항 연산자
- `condition ? true:false`
- 예제 코드 (1)
    ```jsx
    function UserStatus(props) {
      return (
        <div>
          The user is <b>{isLoggedIn ? 'currently' : 'not'}</b> logged in.
        </div>
      );
    }
    ```
- 예제 코드 (2) - 문자열이 아닌 엘리먼트를 렌더링 할 수도 있음
    ```jsx
    return (
      <div>
        {isLoggedIn
          ? <LogoutButton onClick={this.handleLogoutClick} />
          : <LoginButton onClick={this.handleLoginClick} />
        }
      </div>
    );
    ```
    

---

### Component 렌더링 막기
- 리액트에서 null을 리턴하면 렌더링 되지 않음!
- 예제 코드
    ```jsx
    function WarningBanner(props) {
      if (!props.warn) {
        return null;
      }
    
      return (
        <div>Warning!</div>
      );
    }
    ```