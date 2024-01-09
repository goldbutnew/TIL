# Components and Props

## 1. Componets의 Props의 정의

### Components

- 리액트는 컴포넌트 기반의 구조
- 레고 블록 조립하듯 컴포넌트들을 모아서 개발
- 작은 컴포넌트들이 모여서 하나의 컴포넌트를 구성하고 또 이러한 컴포넌트들이 모여서 전체 페이지를 구성
- 하나의 컴포넌트를 반복적으로 사용함으로서 전체 코드의 양을 줄일 수 있음
- 자연스럽게 개발 시간과 유지보수 비용도 줄일 수 있음

### Props(입력) → React component → React element(출력)

- props(Property): 컴포넌트에 전달할 다양한 정보를 담고 있는 자바스크립트 객체

<br>

## 2. Props의 특징 및 사용법

### Props의 특징

- Read-only (읽을 수만 있음)
- 값을 변경할 수 없다
- 다른 props의 값으로 새로 변경하고 싶으면? 새로운 값을 컴포넌트에 전달하여 새로
- 모든 리액트 컴포넌트는 그들의 props에 관해서는 pure 함수 같은 역할을 해야 함
- 모든 리액트는 props를 직접 바꿀 수 없고, 같은 props에 대해서는 항상 같은 결과를 보여줄 것~~~~~~~!

### JS 함수의 속성

- PURE
    
    ```jsx
    function sum(a, b) {
        return a+b
    }
    ```
    
    - a와 b라는 두 개의 파라미터를 받아서 값을 리턴
    - a, b는 변경되지 않음 → 퓨어하다
    - 입력값을 변경하지 않으면 같은 입력값에서는 항상 같은 출력값을 리턴 한다

- IMPURE
    
    ```jsx
    function withdraw(account, amount) {
        account.total -= amount
    }
    ```
    
    - account를 변경함
    
    ### Props 사용법
    
    ```jsx
    function App(props) {
        return (
            <Profile 
                name="goldbtunew"
                introduction="안녕하세요, goldbutnew입니다."
                viewCount={1500}
            />
        )
    }
    ```
    
    - 중괄호를 사용하면 무조건 JS코드
    - props에 값을 넣을 때도, 문자열 외에 정수 변수 다른 컴포넌트들이 들어간다면 중괄호로 감싸 주어야 함
    - 이렇게 되면 이 속성의 값들이 이 컴포넌트의 props로 전달되고 js 객체가 됨
    
    ```jsx
    function App(props) {
        return (
            <Layout
                width={2560}
                height={1440}
                header={
                    <Header title="소플의 블로그입니다." />
                }
                footer={
                    <Footer />
                }
            />
        )
    }
    ```
    
    - Props에 중괄호를 사용해서 Props의 값으로 컴포넌트도 넣을 수 있음
    - 위 예시에서는 리액트 엘리먼트로 header, footer가 들어옴
    

<br>

## 3. Component 만들기 및 렌더링

### Component 만들기

![Untitled](https://github.com/goldbutnew/TIL/assets/149566915/8e33af17-0f9d-4168-9082-dcfcb31ce93b)

### Function Component

```jsx
function Welcome(props) {
    return <h1>안녕, {props.name}</h1>
}
```

- 간단한 코드가 장점

### Class Component

```jsx
class Welcome extends React.Component {
    render() {
        return <h1>안녕, {this.props.name}</h1>
    }
}
```

- 리액트의 모든 클래스 컴포넌트는 React.Component를 상속해서 받는다

### Component의 이름

- 컴포넌트 이름은 항상 대문자로 시작해야 한다
- 리액트는 소문자로 시작하는 컴포넌트를 돔으로 인식함
- 예시
    - HTML div 태그로 인식
        
        ```jsx
        const element = <div />
        ```
        
    - Welcome이라는 리액트 Component로 인식
        
        ```jsx
        const element = <Welcome name="인제" />
        ```
        

### Component 렌더링

- DOM 태그를 사용한 element
    
    ```jsx
    const element = <div />
    ```
    
- 사용자가 정의한 Component를 사용한 element
    
    ```jsx
    const element = <Welcome name="인제" />
    ```
    
- 활용
    
    ```jsx
    // welcome component
    function Welcome(props) {
        return <h1>안녕, {props.name}</h1>
    }
    
    // welcome component에 name값을 넣어 호출해서 렌더링 
    const element = <Welcome name="인제" />
    ReactDOM.render(
        element,
        document.getElementById('root')
    )
    ```
    

### Component 합성

- 여러 개의 컴포넌트를 합쳐서 하나의 컴포넌트를 만드는 것
- 리액트는 컴포넌트 안에 컴포넌트를 쓸 수 있음
- 복잡한 화면을 여러 개의 컴포넌트로 나눠서 구성 가능

### Component 추출

- 복잡한 컴포넌트를 쪼개서 여러 개의 컴포넌트로 만든다
- 컴포넌트 추출 잘 활용하면 재사용성이 올라감
- 재사용성 상승 → 개발 속도 상승

### 추출 예시

```jsx
function Comment(props) {
    return (
        <div className="comment">
            <div className="user-info">
                <img className="avatar"
                    src={props.author.avatarUrl}
                    alt={props.author.name}
                />
                <div className="user-info-name">
                    {props.author.name}
                </div>
            </div>

            <div className="comment-text">
                {props.text}
            </div>

            <div className="comment-date">
                {formaDate(porps.date)}
            </div>

        </div>
    )
}
```

1. avatar 추출하기
    
    ```jsx
    function Avatar(props) {
        return (
            <img className="avatar"
                src={props.user.avatarUrl}
                alt={props.user.name}
            />
        )
    }
    ```
    
    - 재사용성 측면을 고려해서 author를 user로 바꿈
2. avatar 컴포넌트로 변경
    
    ```jsx
    function Comment(props) {
        return (
            <div className="comment">
                <div className="user-info">
                    <Avatar user={props.author} />
                    <div className="user-info-name">
                        {props.author.name}
                    </div>
                </div>
    
                <div className="comment-text">
                    {props.text}
                </div>
    
                <div className="comment-date">
                    {formaDate(porps.date)}
                </div>
    
            </div>
        )
    }
    ```