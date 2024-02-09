# Ajax와 서버
### Ajax

- Asynchronous JavaScript + XML
- JS의 비동기 구조와 ~~XML~~XHR 객체를 활용해 비동기적으로 서버와 통신하여 웹페이지의 일부분만을 업데이트하는 웹개발 기술

### Ajax를 활용한 클라이언트 서버 간 동작

![Untitled](https://github.com/goldbutnew/TIL/assets/149566915/bead0050-7c1e-42b0-8b23-ea6bef2df770)

- **클라이언트** / **서버**
    1. **이벤트 발생**
    2. **XML 객체 생성 및 요청**
    3. **Ajax 요청 처리**
    4. **응답 데이터 생성**
    5. **JSON 데이터 응답** 
    6. **응답 데이터를 활용해 DOM 조작** 
    7. 웹페이지의 일부분만을 다시 로딩
    
<br>

# Ajax with follow
### 프로필 페이지에 axios CDN 작성
```jsx
	<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
  <script>
  </script>
</body>
</html>
```

### form 요소 선택을 위해 id 속성 지정 및 선택
- action과 method 속성은 axiois로 요청이 대체되기 때문에 삭제한다
```html
<form id='follow-form' data-user-id="{{ person.pk }}">
  {% csrf_token %}
  {% if request.user in person.followers.all %}
    <input type="submit" value="Unfollow">
  {% else %}
    <input type="submit" value="Follow">
  {% endif %}
</form>
```
```jsx
const formTag = document.querySelector('#follow-form')
```

### form 요소에 이벤트 핸들러 작성 및 submit 이벤트의 기본 동작 취소
```jsx
formTag.addEventListener('submit', function (event) {
	event.preventDefault()
})
```

### axios 요청
```jsx
formTag.addEventListener('submit', function (event) {
  event.preventDefault()
  axios({
    url: `/accounts/${}/follow/`,
    method: 'post',
  })
})
```

- 과제
    1. url에 작성할 user pk는 어떻게 작성? → HTML에서 JS으로 가져오기
        ```jsx
        <form id='follow-form' data-user-id="{{ person.pk }}">
          ...
        </form>
        ```
    2. csrftoken은 어떻게 보내야 할까?
        ```jsx
        formTag.addEventListener('submit', function (event) {
        		event.preventDefault()
        
            const userId = formTag.dataset.userId
        		...
        })
        ```
- `data-*` 속성
    - 사용자 지정 데이터 특성을 만들어 임의의 데이터를 HTML과 DOM 사이에서 교환할 수 있는 방법
    - 사용예시
        ```jsx
        <div data-my-id="my-data"></div>
        
        <script>
        	const myId = evenet.target.dataset.myId
        </script>
        ```
        - 모든 사용자 지정 데이터는 JS에서 dataset 속성을 통해 사용
        - 주의사항
            - 대소문자 여부에 상관없이 `xml` 문자로 시작 불가
            - 세미콜론 포함 불가
            - 대문자 포함 불가
            - JS MDN
              [https://developer.mozilla.org/ko/docs/Learn/HTML/Howto/Use_data_attributes](https://developer.mozilla.org/ko/docs/Learn/HTML/Howto/Use_data_attributes)
                

### 요청 url 작성 마무리
```jsx
formTag.addEventListener('submit', function (event) {
  event.preventDefault()

	const userId = formTag.dataset.userId

  axios({
    url: `/accounts/${userId}/follow/`,
    method: 'post',
  })
})
```