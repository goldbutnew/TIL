# Most Common Hooks

## useState

- state를 사용하기 위한 hook

### useState() 사용법

- `const [변수명, set 함수명] = useState(초기값)`
- 예시
    
    ```jsx
    import React, { useState } from "react"
    
    // 카운트를 함수의 변수로 사용하게 되면 버튼 클릭 시 카운트 값이 증가할 수 있지만 재 렌더링 하지 않아 새로운 카운트의 값이 증가하지는 않을 수도 있음
    function Counter(props) {
        // var count = 0
    
        const [count, setCount] = useState(0)
    
        return (
            <div>
                <p>총 {count}번 클릭했습니다.</p>
                <button onClick={() => setCount(count + 1)}>
                    클릭
                </button>
                {/* <button onClick={() => count++}>
                    클릭
                </button> */}
            </div>
        )
    }
    ```
    
- 다만, class 컴포넌트에서는 setState 함수 하나를 사용해서 모든 state 함수를 다 업데이트 할 수 있었지만, useState 함수는 변수 각각에 대해 set 함수가 따로 존재

<br>

## useEffect

- side effect를 사용하기 위한 hook
- side effect = 부작용
- 그러나 리액트에서 말하는 side effect는 효과, 영향의 의미로 사용됨
- 서버에서 데이터를 받아오거나, 수동으로 DOM 변경하는 작용들을 의미
- 다른 컴포넌트에 영향을 미칠 수 있으며, 렌더링 중에는 작업이 완료될 수 없기 때문에 effect라고 부름
- useEffect hooks은 하나의 컴포넌트에 여러 개 사용 가능

### useEffect() 사용법
- `useEffect(이펙트 함수, 의존성 배열)`
- effect function이 mount, unmount 시에 단 한 번씩만 실행시키려면?
    - `useEffect(이펙트 함수, [])`
    - 의존성 배열에 빈 배열을 넣으면 됨!
- 의존성 배열을 아예 생략하면?
    - `useEffect(이펙트 함수)`
    - 업데이트 될 때마다 호출됨
- 총정리
    ```jsx
    useEffect(() => {
        // 컴포넌트가 마운트 된 후,
        // 의존성 배열에 있는 변수들 중 하나라도 값이 변경되었을 때 실행됨
        // 의존성 배열에 빈 배열([])을 넣으면 마운트와 언마운트 시 단 한 번씩만 실행됨
        // 의존성 배열 생략 시 컴포넌트 업데이트 시마다 실행됨
        
        return () => {
            // 컴포넌트가 마운트 해제되기 전에 실행됨
        }
    }, [의존성 변수1, 의존성 변수2, ...])
    ```

- 예시
    ```jsx
    import React, { useState, useEffect } from "react"
    
    function Counter(props) {
        const [count, setCount] = useState(0)
    
        // componentDidMount, componentDidUpdate와 비슷하게 동작합니다
        useEffect(() => {
            // 브라우저 API를 사용해서 document의 title을 업데이트
            document.title = `You clicked ${count} times`
        })
    
        return (
            <div>
                <p>총 {count}번 클릭했습니다.</p>
                <button onClick={() => setCount(count + 1)}>
                    클릭
                </button>
            </div>
        )
    }
    ```
- componentWillUnmount와 동일한 기능은 어떻게 구현?
    ```jsx
    import React, { useState, useEffect } from "react"
    
    function UserStatus(Props) {
        const [isOnline, setIsOnline] = useState(null)
    
        function handleStatusChange(status) {
            setIsOnline(status.isOnline)
        }
    
        useEffect(() => {
            ServerAPI.subscribeUserStatus(props.user.id, handleStatusChange)
            // 컴포넌트가 unmount 될 때 호출됨
            return () => {
                ServerAPI.unsubscriveUserStatus(props.user.id, handleStatusChange)
            }
        })
    
        if (isOnline === null) {
            return '대기 중...'
        }
        return isOnline ? '온라인' : '오프라인'
    }
    ```

<br>

## useMemo
- Memoized value를 리턴하는 Hook
- Memoization
    - 최적화를 위해 사용하는 개념
    - 비용이 높은 함수의 호출 결과를 저장해 두었다가, 같은 입력값의 함수를 호출하면 이전의 호출을 불러옴으로서 연산량을 줄일 수 있음!
- 빠른 렌더링 속도를 얻을 수 있음~~~!
- 유념할 점은 useMemo는 렌더링이 일어날 때 실행됨
- 일반적으로 렌더링이 일어날 때 실행돼서는 안 되는 함수는 넣으면 안 됨

### useMemo() 사용법
```jsx
const memoizedValue = useMemo(
    () => {
        // 연산량이 높은 작업을 수행하여 결과를 반환
        return computeExpensiveValue(의존성 변수1, 의존성 변수2)
    },
    [의존성 변수1, 의존성 변수2]
)
```
- 의존성 배열을 넣지 않을 경우, 매 렌더링마다 함수가 실행됨
    ```jsx
    const memoizedValue = useMemo(
        () => computeExpensiveValue(a, b)
    )
    ```
    - 고로, useMemo Hook에 의존성 배열을 넣지 않는 것은 아무런 의미가 없음
- 의존성 배열이 빈 배열인 경우
    ```jsx
    const memoizedValue = useMemo(
        () => {
            return computeExpensiveValue(a, b)
        },
        []
    )
    ```
    - 컴포넌트 마운트 시에만 호출됨 → 마운트 이후에는 값 변경 x
    - 마운트 시점에만 한 번 계산하면 되는 경우? 근데 이런 경우 잘 없긴 함

<br>

## useCallback
- useMemo hook과 유사하지만 값이 아닌 함수를 반환
- useMemo와 마찬가지로 함수와 의존성 변수를 파라미터로 받음
- 의존성 변수 중 하나라도 변경되면 memoization 된 콜백함수를 반환

### useCallback() 사용법
```jsx
const memoizedCallback = useCallback(
    () => {
        doSomething(의존성 변수1, 의존성 변수2)
    },
    [의존성 변수1, 의존성 변수2]
)
```

- 동일한 역할을 하는 두 줄의 코드
    ```jsx
    useCallback(함수, 의존성 배열)
    
    useMemo(() => 함수, 의존성 배열)
    ```
    
- 만약 useCallback hook을 사용하지 않는다면?
    ```jsx
    import { useState } from "react"
    
    function ParentComponent(props) {
        const [count, setCount] = useState(0)
    
        // 재렌더링 될 때마다 매번 함수가 새로 정의됨
        const handleClick = (event) => {
            // 클릭 이벤트 처리
        }
    
        return (
            <div>
                <button
                    onClick={() => {
                        setCount(count + 1)
                    }}
                >
                    {count}
                </button>
                <ChildComponent handleClick={handleClick} />
            </div>
        )
    }
    ```
    
- 사용한다면?
    ```jsx
    ...
        // 컴포넌트가 마운트 될 때만 함수가 정의됨
        const handleClick = useCallback((event) => {
            // 클릭 이벤트 처리
        }, [])
    
    ```
    - 컴포넌트가 처음 마운트되는 시점에만 함수가 정의됨!

<br>

## useRef

- Reference를 사용하기 위한 Hook
- 특정 컴포넌트에 접근할 수 있는 객체
- refObject.current
    - `.current`: 현재 참조하고 있는 Element
- 쉽게 말해, 변경 가능한 current라는 속성을 가진 하나의 상자

### useRef() 사용법

```jsx
const refContainer = useRef(초깃값)
```

- 파라미터로 초기값을 넣으면 해당 초기값으로 초기화된 ref 객체를 반환
- 만약 초기값이 null이라면 current의 값이 null인 레퍼런스 객체 반환
- 이렇게 반환된 ref 객체는 컴포넌트의 라이프타임 전체에 걸쳐 유지됨
- 활용 예시
    ```jsx
    function TextInputWithFocusButton(props) {
        const inputElem = useRef(null)
    
        const onButtonClick = () => {
            // `current`는 마운트된 input element를 가리킴
            inputElem.current.focus()
        }
    
        return (
            <>
                <input ref={inputElem} type="text" />
                <button onClick={onButtonClick}>
                    Focus the input
                </button>
            </>
        )
    }
    ```
    - 실제 element에 접근하여 포커스 함수 호출

### ref 속성과 useRef() hook 차이?

- 리액트에서는 아래와 같이 코드를 작성하면 노드가 변경될 때마다 myref의 current 속성에 현재 해당하는 DOM 노드를 저장
    ```jsx
    <div ref={myRef} />
    ```
- ref 속성과 기능은 비슷하지만 useRefHook은 클래스 **instance 필드**를 사용하는 것과 유사하게 다양한 변수를 저장할 수 있다는 장점이 있음
- 이런 것이 가능한 이유: useRefHook은 일반적인 자바스크립트 객체를 리턴
- useRef() hook은 매번 렌더링 될 때마다 항상 같은 레퍼런스 객체를 반환
- useRef() hook은 내부의 데이터가 변경되었을 때, 별도로 알리지 않음
- 고로, 커런트 속성을 변경한다고 해서 재렌더링이 일어나지 않음
- 그렇다면 돔 노드의 변화를 알기 위한 가장 기초적인 방법? → callback ref 사용
    - ref가 다른 노드에 연결될 때마다 callback 함수 호출