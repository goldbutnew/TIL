# About Hooks

### Function Component vs Class Component

- Class Component
    - 생성자에서 state 정의
    - setState() 함수를 통해 state 업데이트
    - Lifecycle methods 제공
    - 모든 게 명확하게 정의되어 있기 때문에 잘 가져다 쓰기만 하면 됨
- Function Component
    - state 사용 불가
    - Lifecycle에 따른 기능 구현 불가
    - 함수 컴포넌트의 기능을 지원하기 위해 등장한 것이 바로 **Hooks**

### Hooks의 정의

- 갈고리
- 프로그래밍에서 Hooks이란 원래 존재하는 어떤 기능에 마치 갈고리를 거는 것처럼 끼어들어 같이 수행되는 것을 의미
- Function Component에 끼어들어, State 관련 함수, Lifecycle 관련 함수, 최적화 관련 함수를 수행함
- 개발자가 직접 custom hook  을 만들어서 사용할 수도 있음
- 다만 이름 앞에 use를 붙여 hook이라는 것을 나타내 줘야 함