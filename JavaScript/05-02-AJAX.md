# AJAX
- Asynchronous JavaScript + ~~XML~~**JSON**
- JS의 비동기 구조와 XML 객체를 활용해 비동기적으로 서버와 통신하여 웹 페이지의 일부분만을 업데이트하는 웹 개발 기술
- X가 XML을 의미하긴 하지만 요즘은 더 가벼운 용량과 JS의 일부라는 장점 때문에 JSON을 더 많이 사용

### XMLHttpRequest 객체 (XHR )
- 서버와 상호작용 할 때 사용하며 페이지의 새로고침 없이도 URL에서 데이터를 가져올 수 있음
- 사용자의 작업을 방해하지 않고 페이지의 일부를 업데이트
- 주로 AJAX 프로그래밍에 많이 사용됨

### 이벤트 핸들러는 비동기 프로그래밍의 한 형태
- 이벤트가 발생할 때마다 콜백함수 제공
- XMLHttpRequest(XHR)는 JS를 사용하여 서버에 HTTP 요청을 할 수 있는 객체
- HTTP 요청은 응답이 올 때까지의 시간이 걸릴 수 있는 작업이라 비동기 API이며, 이벤트 핸들러를 XHR 객체에 연결해 요청의 진행 상태 및 최종 완료에 대한 응답을 받음

<br>

## Axios
- JavaScript에서 사용되는 HTTP 클라이언트 라이브러리
- 서버와의 HTTP 요청과 응답을 간편하게 처리할 수 있도록 도와주는 도구

### Axios 구조
```jsx
// axios는 promise 객체
axios({
  method: 'get',
  url: URL,
	data: {
		name: 'geumhyunlee'
	}
})
	// 이전 요청이란? axios
	.then(이전 요청에 성공하면 수행할 콜백함수)
	.catch(이전 요청에 실패하면 수행할 콜백함수)
```
- get, post 등 여러 http request method 사용 가능
- `then` 메서드를 사용해서 **성공하  면 수행할 로직**을 작성
- `catch` 메서드를 사용해서 **실패하면 수행할 로직**을 작성


### 고양이 사진 가져오기 실습

- 기본
    ```jsx
    <body>
      <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
      <script>
        const URL = 'https://api.thecatapi.com/v1/images/search'
        axios({
          method: 'get',
          url: URL,
        })
          .then((response) => {
            console.log(response)
            console.log(response.data)
          })
          .catch((error) => {
            console.log(error)
            console.log('실패했다옹')
          })
        console.log('야옹야옹')
      </script>
    </body>
    ```  
- 심화
    ```jsx
    <body>
      <button>냥냥펀치</button>
    
      <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
      <script>
        const URL = 'https://api.thecatapi.com/v1/images/search'
        const btn = document.querySelector('button')
    
        const getCats = function() {
        axios({
          method: 'get',
          url: URL,
        })
          .then((response) => {
            imgUrl = response.data[0].url
            imgElem = document.createElement('img')
            imgElem.setAttribute('src', imgUrl)
            document.body.appendChild(imgElem)
          })
          .catch((error) => {
            console.log(error)
            console.log('실패했다옹')
          })
        console.log('야옹야옹')
      }
    
      btn.addEventListener('click', getCats)
    
      </script>
    </body>
    ```
    
### 정리
- axios는 브라우저에서 비동기 데이터 통신을 가능하게 하는 라이브러리
    - 브라우저를 위해 XMLHttpRequest 생성
- 같은 방식으로 DRF로 만든 API 서버로 요청을 보내서 데이터를 받아온 후 처리할 수 있도록 함