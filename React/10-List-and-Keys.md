# List and Keys

## List와 Key

### List

- 같은 아이템을 순서대로 모아놓은 것

### Array

- 리스트에 사용되는 자료 구조
- JS의 변수나 객체들을 하나의 변수로 묶어 놓은 것
- 예제 코드
    ```jsx
    const number = [1, 2, 3, 4, 5]
    ```
    

### Key

- 각 객체나 아이템을 구분할 수 있는 고유한 값
- 아이템들을 구분하기 위한 고유한 문자열

<br>

## 여러 개의 Component 렌더링 하기

- 배열과 키를 사용하여 반복되는 여러 개의 컴포넌트들을 쉽게 렌더링할 수 있음

### map()

- 배열에 들어 있는 각 변수에 어떤 처리를 한 뒤 리턴하는 것
- 예제 코드 (1)
    ```jsx
    const doubled = numbers.map((number) => number * 2)
    ```
    
- 예제 코드 (2) - 리액트에서의 map 함수
    ```jsx
    const numbers = [1, 2, 3, 4, 5];
    const listItems = numbers.map((number) =>
      <li>{number}</li>
    )
    
    ReactDOM.render(
        <ul>{listItems}</ul>,
        document.getElementById('root')
    )
    ```
    

### 기본적인 List Component
```jsx
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li>{number}</li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<NumberList numbers={numbers} />);
```
- 그러나 경고문 등장 → 리스트의 각 아이템은 무조건 고유한 키를 가지고 있어야 한다는 뜻
- 키가 없어서 경고문 출력!

<br>

## List의 Key

### key

- 아이템들을 구분하기 위한 고유한 문자열
- 리스트에서 어떤 아이템이 변경, 추가 또는 제거되었는지 구분
- 리액트에서의 key 값은 같은 엘리먼트 사이에서만 고유한 값이면 된다
- 

### key로 값을 사용하는 경우
```jsx
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>
    {number}
  </li>
);
```
- 지금처럼 배열의 값이 중복되지 않는 경우에는 정상 작동
- numbers 배열에 중복된 숫자가 들어있다면 key값도 중복되기 때문에 고유해야 한다는 조건 충족 불가

### key로 id를 사용하는 경우
```jsx
const todoItems = todos.map((todo) =>
  <li key={todo.id}>
    {todo.text}
  </li>
);
```
- 보통 아이디 값 그 자체가 고유한 값이라 사용하기 적합

### key로 index를 사용하는 경우
```jsx
const todoItems = todos.map((todo, index) =>
  // 아이템들의 고유한 id가 없을 때만 사용 추천
  <li key={index}>
    {todo.text}
  </li>
);
```

- 배열 내에서 현재 아이템의 인덱스를 의미
- 다만 배열에서 아이템의 순서가 바뀔 수 있는 경우가 있기 때문에 키값으로 인덱스를 사용하는 것을 권장하지 않음
- 고유한 아이디가 없을 경우만 사용~
- 리액트에선 키를 명시적으로 넣어 주지 않으면 기본적으로 이 인덱스 값을 키값으로 사용

### (중요) map() 함수 안에 있는 Elements는 꼭 key가 필요!