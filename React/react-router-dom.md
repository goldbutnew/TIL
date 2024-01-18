# react-router-dom

### 라우트 구성
```jsx
<BrowserRouter>
    <Routes>
        <Route index element={<MainPage />} />
        <Route path="post-write" element={<PostWritePage />} />
        <Route path="post/:postId" element={<PostViewPage />} />
    </Routes>
</BrowserRouter>
```
- `BrowserRouter`: 웹브라우저에서 리액트 라우터를 사용하여 라우팅을 할 수 있도록 해 주는 컴포넌트(웹브라우저 히스토리 기능을 통해 뒤로가기 버튼을 눌렀을 때 이전 페이지를 찾음)
- `Routes`: 여러 개의 라우트 컴포넌트를 자식으로 가짐
- `Route`:  라우츠 컴포넌트의 하위 컴포넌트로 path와 element라는 props를 가짐
    - `path`: 경로
    - `element`: 경로가 일치할 경우 렌더링할 엘리먼트
- 예제 코드
    ```jsx
    <BrowserRouter>
        <MainTitleText>나의 미니 블로그</MainTitleText>
        <Routes>
            <Route index element={<MainPage />} />
            <Route path="post-write" element={<PostWritePage />} />
            <Route path="post/:postId" element={<PostViewPage />} />
        </Routes>
    </BrowserRouter>
    ```
    - `:postId`: 파라미터 동적 변환
        - useParams hook을 사용해 아이디로 해당 값을 불러옴

### 페이지 간 이동

- `useNavigate()`
    - react-router-dom이 페이지 간 이동을 위해 제공하는 hook
    - 예제 코드
        ```jsx
        function SampleNavigate(props) {
            const navigate = useNavigate()
        
            const moveToMain = () => {
                navigate("/")
            }
        
            return (
                ...
            )
        }
        ```
        

### 참고

- [https://reactrouter.com/en/main](https://reactrouter.com/en/main)