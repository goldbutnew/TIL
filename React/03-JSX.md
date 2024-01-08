# JSX

### JSX란?

- A syntax extension to JavaScript
- JavaScript + XML/HTML

### JSX 예제 코드

```jsx
const element = <h1>Hello, wordl!</h1>
```

### JSX 역할

- JSX는 내부적으로 html, xml 코드를 JS로 변환하는 과정을 거친다
- 그래서 우리가 HTML로 작성해도 JS 코드가 최종적으로 나오는 것

### JSX를 사용한 코드

```jsx
React.createElement(
  type,
  [props],
  [...children]
)
```

```jsx
class Hello extends React.Component {
  render() {
    return <div>Hello {this.props.toWhat}</div>
  }
}

ReactDOM.render(
	<Hello toWhat='World' />
	document.getElementById('root')
)
```

### JSX를 사용하지 않은 코드

```jsx
class Hello extends React.Component {
  render() {
    return React.createElement('div', null, `Hello ${this.props.toWhat}`);
  }
}

ReactDOM.render(
  React.createElement(Hello, { toWhat: 'World' }, null),
  document.getElementbyId('root')
);
```

### JSX 사용 유무 비교

```jsx
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>

// JSX를 사용하지 않은 코드
const element = React.createElement(
  'h1',
  { className: 'greeting' },
  'Hello, world!'
)
```

- `React.createElement()`의 결과로 아래와 같은 객체가 생성됨
    
    ```jsx
	const element = {
		type: 'h1',
		props: {
			className: 'greeting',
			children: 'Hello, world!'
		}
	}
    ```
    

- `createElement()` 함수의 파라미터는?
    
    ```jsx
	React.createElement(
		type,
		[props],
		[..children]
	)
    ```
    

### JSX 장점

- 간결한 코드
    
    ```jsx
    // JSX 사용한 코드
    <div>Hello, {name}</div>
    
    // JSX 사용 안 함
    React.createElement('div', null, `Hello, ${name}`)
    ```
    
- 가독성 향상
- 버그를 발견하기 쉬움
- Injection Attacks 방어
    
    ```jsx
    const title = responser.potentiallyMaliciousInput
    
    // 이 코드는 안전합니다
    const element = <h1>{title}</h1>
    ```
    

### JSX 사용법

- JS + XML/HTML
- JS 코드를 쓰고 싶으면 중괄호{}로 묶어 주면 됨
    
    ```jsx
	function getGreeting(user) {
		if (user) {
			return <h1>Hello, {formatName(user)}!</h1>
		}
		return <h1>Hello, Stranger.</h1>
	}
    ```
    
- HTML 중간이 아닌 태그의 속성에 값을 넣고 싶을 때는?
    
    ```jsx
    // 큰따옴표 사이에 문자열 넣기
    const element = <div tabIndex="0"></div>
    
    // 중괄호 사이에 자바스크립트 코드를 넣으면 됨!
    const element = <img src={user.avatarUrl}></img>
    ```
    
- 자식(children)을 정의하는 방법
    
    ```jsx
	const element = (
		<div>
			<h1>안녕하세요</h1>
			<h2>열심히 리액트를 공부해 봅시다</h2>
		</div>
	)
    ```