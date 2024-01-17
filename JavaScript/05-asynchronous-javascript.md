# 비동기

## 동기
- synchronous
- 프로그램의 실행 흐름이 순차적으로 진행
- 하나의 작업이 완료된 후에 다음 작업이 실행되는 방식

### 동기 예시
1. 메인 작업이 모두 수행되어야 마지막 작업이 수행됨
    ```jsx
    print('첫 번째 작업')
    for i in range(10):
    		print('메인 작업')
    print('마지막 작업')
    ```
    
2. 함수의 작업이 완료될 때까지 기다렸다가 값을 반환해야 계속 진행할 수 있음 (동기 함수)
    ```jsx
    const makeGreeting = function(name) {
    	return `Hello, my name is ${name}!`
    }
    
    const name = 'Alice'
    const greeting = makeGreeting(name)
    console.log(greeting) // 'Hello, my name is Alice!'
    ```

<br>    

## 비동기
- Asynchronous
- 프로그램의 실행 흐름이 순차적이지 않으며, 작업이 완료되기를 기다리지 않고 다음 작업이 실행되는 방식
- 작업의 완료 여부를 신경쓰지 않고 **동시에 다른 작업들을 수행**

### Asynchronous 특징
- 병렬적 수행
- 당장 처리를 완료할 수 없고 시간이 필요한 작업들은 별도로 요청을 보낸 뒤 응답이 빨리 오는 작업부터 처리

    ![Untitled](https://github.com/goldbutnew/TIL/assets/149566915/d18af295-c558-467f-a03b-b59947520684)
    

### Asynchronous 예시
```jsx
<script>
  const slowRequest = function (callBack) {
    console.log('1. 오래 걸리는 작업 시작...')
		// 3초를 기다렸다가 콜백 함수를 호출하는 함수
    **setTimeout(function () { 
      callBack()
    }, 3000)
  }**

  const myCallBack = function () {
    console.log('2. 콜백함수 실행됨')
  }

  slowRequest(myCallBack)

  console.log('3. 다른 작업 실행')
</script>
```
![Untitled 1](https://github.com/goldbutnew/TIL/assets/149566915/794bf075-fe68-4aff-99fe-7cc57088d16f)

<br>

# JavaScript와 비동기

### Single Thread 언어, JavaScript
- Thread란?
    - 작업을 처리할 때 실제로 작업을 수행하는 주체
    - multi-thread라면 업무를 수행할 수 있는 주체가 여러 개
- JS는 한 번에 여러 일을 수행할 수 없는 Single Thread 언어
    - 그렇다면 어떻게 비동기 처리를?

### JS Runtime
- JavaScript가 동작할 수 있는 환경(Runtime)
- JS 자체는 Single Thread이므로 비동기 처리를 할 수 있도록 도와주는 환경 필요
- JS에서 비동기와 관련한 작업은 ‘브라우저’ 또는 ‘Node’와 같은 환경에서 처리

### 비동기 처리 동작 요소
- Call Stack
    - 요청이 들어올 때마다 순차적으로 처리하는 stack(LIFO)
    - 기본적인 JS의 Single Thread 작업 처리
- Web API
    - JS 엔진이 아닌 브라우저에서 제공하는 runtime 환경
    - 시간이 소요되는 작업을 처리 (setTimeout, DOM Event, AJAX 요청 등)
- Task Queue (Callback Queue)
    - 비동기 처리된 Callback 함수가 대기하는 Queue(FIFO)
- Event Loop
    - 테스크(작업)가 들어오길 기다렸다가 태스크가 들어오면 이를 처리
    - 처리할 태스크가 없는 경우엔 잠드는, 끊임없이 돌아가는 JS 내 루프
    - Call Stack과 Task Queue를 지속적으로 모니터링
    - Call Stack이 비어 있는지 확인 후 비어 있다면 Task Queue에서 대기 중인 오래된 작업을 Call Stack이 Push