# JavaScript and DOM

# DOM

## 개요

### 웹 브라우저에서의 JavaScript

- 웹 페이지의 동적인 기능을 구현

### JavaScipt 실행 환경 종류

1. HTML script 태그
    
    ```html
    <body>
      <script>
        console.log('hello world')
      </script>
    </body>
    ```
    
2. js 확장자 파일
    
    ```html
    <body>
      <script src="hello.js">
      </script>
    </body>
    ```
    
    ```jsx
    console.log('hello')
    ```
    
3. 브라우저 Console
    
    ![1](https://github.com/goldbutnew/TIL/assets/149566915/6bc46a47-b11d-4743-91eb-8c78aafab472)
    

### DOM

- The Docoument Object Model
- 웹 페이지(Document)를 구조화된 객체로 제공하여 프로그래밍 언어가 페이지 구조에 접근할 수 있는 방법을 제공
- 문서 구조, 스타일, 내용 등을 변경할 수 있도록 함

### DOM 특징

- DOM에서 모든 요소, 속성, 텍스트는 하나의 객체
- 모두 document 객체의 자식으로 구성됨
    
    ![2](https://github.com/goldbutnew/TIL/assets/149566915/7c262587-4226-4830-8550-3b551e21560d)
    

### DOM tree

- 브라우저는 HTML 문서를 해석하여 DOM tree라는 객체 트리로 구조화
- 객체 간 상속 구조가 존재

```jsx
<!DOCTYPE html>
<html lang="en">

<head>
<title>Document</title>
</head>

<body>
	<h1>Heading</h1>
  <a href="https://www.google.com/">google</a>
</body>

</html>
```

### DOM 핵심

- 문서의 요소들을 객체로 제공하여 다른 프로그래밍 언어에서 접근하고 조작할 수 있는 방법을 제공하는 API

## document 객체

- 웹페이지 객체
- DOM Tree의 진입점
- 페이지를 구성하는 모든 객체 요소를 포함

### document 객체 예시

- HTML의 title 변경하기
    
    ![3](https://github.com/goldbutnew/TIL/assets/149566915/be8e2139-2002-4f7c-95a7-92f72a29c62f)
    

# DOM 선택

### DOM 조작 시 기억해야 할 것

- 웹 페이지를 동적으로 만들기 == 웹 페이지를 조작하기
    - 조작 순서
        1. 조작하고자 하는 요소를 **선택**(또는 탐색)
        2. 선택된 요소의 콘텐츠 또는 속성을 **조작**

## 선택 메서드

- `document.querySelector()` : 요쇼 한 개 선택
- `document.querySelectorAll()` : 요소 여러 개 선택

### document.**querySelector(selector)**

- 제공한 선택자와 일치하는 element 한 개 선택
- 제공한 CSS selector를 만족하는 첫 번째 element 객체를 반환(없다면 null 반환)

### document.**querySelectorAll(selector)**

- 제공한 선택자와 일치하는 여러 element를 선택
- 제공한 CSS selector를 만족하는 NodeList를 반환

### DOM 선택 실습

```html
<body>
  <h1 class="heading">DOM 선택</h1>
  <a href="https://www.google.com/">google</a>
  <p class="content">content1</p>
  <p class="content">content2</p>
  <p class="content">content3</p>
  <ul>
    <li>list1</li>
    <li>list2</li>
  </ul>
  <script>
  console.log(document.querySelector('.heading'))
  console.log(document.querySelector('.content'))
  console.log(document.querySelectorAll('.content'))
  console.log(document.querySelectorAll('ul > li'))
  </script>
</body>
```

![4](https://github.com/goldbutnew/TIL/assets/149566915/59f02b3c-e2c6-4d65-bfc7-b95992229706)


# DOM 조작

## 속성 조작

### ‘classList’ property

- 요소의 클래스 목록을 DOMTokenList(유사 배열) 형태로 반환

### 클래스 속성 조작 메서드 (classList)

- `element.classList.**add()**`
    - 지정한 클래스 값을 추가
- `element.classList.**remove()**`
    - 지정한 클래스 값을 제거
- `element.classList.**toggle()**`
    - 클래스가 존재한다면 제거하고 flase를 반환
    - 존재하지 않는다면 클래스를 추가하고 true 반환

### 일반 속성 조작 메서드

- `Element.**getAttribute()**`
    - 해당 요소에 지정된 값을 반환(조회)
- `Element.**setAttrubute(name, value)**`
    - 지정된 요소의 속성값을 설정
    - 속성이 이미 있으면 기존값을 갱신(그렇지 않으면 지정된 이름과 값으로 새 속성이 추가)
- `Element.**removeAttribute()**`
    - 요소에서 지정된 이름을 가진 속성 제거

### 속성 조작 실습

```jsx

<script>
  // 속성 조작
  // 1. 클래스 속성 조작
  const h1tag = document.querySelector('.heading')
  console.log(h1tag)

  console.log(h1tag.classList)
  h1tag.classList.add('red')

  console.log(h1tag.classList)
  h1tag.classList.remove('red')

  h1tag.classList.toggle('red')

  // 2. 일반 속성 조작
  const aTag = document.querySelector('a')
  aTag.setAttribute('href', 'http://www.naver.com/')

  aTag.removeAttribute('href')
  console.log(aTag.getAttribute('href'))

</script>
```

## HTML 콘텐츠 조작

### `textContent` property

- 요소의 텍스트 콘텐츠를 표현
- <p> lorem </p>