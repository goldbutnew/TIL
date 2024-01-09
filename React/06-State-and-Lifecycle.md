# State and Lifecycle

## 1. State

- 상태
- 리액트에서의 상태: 리액트 컴포넌트의 상태
- 하지만 정상/비정상이 아닌 리액트 컴포넌트의 데이터에 의미가 더 가까움
- 리액트 컴포넌트의 변경 가능한 데이터
- state는 정의되어 있는 것이 아닌 개발자가 정의
- 렌더링이나 데이터 흐름에 사용되는 값만 state에 포함시켜야 함
    - state 변경으로 재렌더링 할 때 관련없는 값을 포함하면 성능 저하시킬 수 있음
    - 그렇지 않은 값은 컴포넌트의 인스턴스 필드로 정의하면 됨
- state는 JS 객체이다
- state는 직접 수정할 수 없다(하면 안 된다)

### State 예제 코드 (1)

```jsx
class LikeButton extends React.Component {
    constructor(props) {
        super(props)
        
        this.state = {
            liked: flase
        }
    }
}
```

- 모든 class component에는 constructor라는 이름의 함수가 존재
- `constructor`: 생성자
- 클래스가 생성될 때 실행됨
- 생성자 코드에는 this.state라는 코드가 나오고 현재 컴포넌트의 state를 정의

### State 예제 코드 (2)

```jsx
// state를 직접 수정(잘못된 사용법)
this.state = {
    name: 'goldbutnew'
}

// setState 함수를 통한 수정 (정상적인 사용법)
this.setState({
    name: 'goldbutnew'
})
```

<br>

## 2. Lifecycle

- 리액트 컴포넌트의 생명주기
- 컴포넌트가 생성되는 시점과 사라지는 시점이 정해져 있음
- Mounting → Updating → Unmounting
- 상위 컴포넌트에서 현재 컴포넌트를 더 이상 화면에 표시하지 않게 될 때 Unmounting 됨
- 다른 생명주기 함수도 존재함! 하지만 이제는 거의 사용되지 않아서 pass
- (중요) component가 계속 존재하는 것이 아니라, 시간의 흐름에 따라 생성되고 업데이트 되다가 사라짐