# Rules of Hooks and Custom Hook

## Hook의 규칙

### 1. Hook은 무조건 최상위 레벨에서만 호출해야 한다

- 최상위 레벨이란? React 함수 컴포넌트의 최상위 레벨을 의미
- 반복문이나 조건문 또는 중첩된 함수들 안에서 Hook을 호출하면 안 됨
- Hook은 컴포넌트가 렌더링될 때마다 매번 같은 순서로 호출되어야 함
- 이렇게 해야 React가 다수의 useState hook과 useEffect hook에 호출해서 컴포넌트의 state를 올바르게 관리할 수 있음
- 잘못된 Hook 사용법 예시
    - if문의 조건이 참인 경우에만 useEffect hook 호출
        
        ```jsx
        import { useEffect } from "react"
        
        function MyComponent(props) {
            const [name, setName] = useState('유경')
        
            if (name !== '') {
                useEffect(() => {
                    ...
                })
            }
        }
        ```
        
        - hook이 같은 순서대로 호출되는 것이 아닌 조건문의 결과에 따라 달라짐으로서 잘못된 코드

### 2. 리액트 함수 컴포넌트에서만 Hook을 호출해야 함

- 일반적인 JS 함수에서 호출하면 안 됨
- React 함수 컴포넌트나 직접 만든 Custom hook에서만 가능
- 이 규칙에 따라 React 컴포넌트에 있는 state와 관련된 모든 로직은 소스코드를 통해 명확하게 확인 가능해야 함

+) `eslint-plugin-react-hooks`: hook의 규칙을 따르도록 강제해 주는 플러그인 

## Custom Hook

- 사용자가 직접 만들어서 쓰는 hook
- 이름이 use로 시작하고 내부에서 다른 Hook을 호출하는 하나의 JS 함수 (use로 시작하지 않으면 특정 함수 내부에서 hook을 호출하는지 알 수 없음)
- 두 개의 JS 함수에서 하나의 로직을 공유하도록 하고 싶을 때에는 새로운 하나를 만드는 방법을 사용
- React 함수 컴포넌트와 hook 모두 함수이기 때문에 동일한 방법을 사용
- 여러 개의 컴포넌트에서 하나의 custom hook을 사용할 때 컴포넌트 내부에 있는 모든 state와 effects는 전부 분리되어 있다
- custom hook의 호출 또한 완전히 독립적