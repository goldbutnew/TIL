# Forms
- 양식
- 텍스트 입력 뿐 아니라 체크박스, 셀렉트 등 사용자에게 입력받는 모든 것
- 사용자로부터 입력을 받기 위해 사용

### React의 Form vs HTML의 Form

![Untitled](https://github.com/goldbutnew/TIL/assets/149566915/7dc8d49c-4ad0-4880-9f26-6261bf60c3f3)


- 리액트: 컴포넌트의 내부에서 state를 통해 데이터를 관리
    ```jsx
    function NameForm(props) {
        const [value, setValue] = useState('')
    
        // event: 이벤트 객체
        // event.target: 현재 발생한 이벤트의 타겟
        // event.target.value: 해당 타겟의 value 속성값
        const handleChange = (event) => {
            setValue(event.target.value)
        }
    
        const handleSubmit = (event) => {
            alert('입력한 이름:' + value)
            event.preventDefault()
        }
    
        // onSubmit, OnChange는 react문법?
        return (
            <form onSubmit={handleSubmit}>
                <label>
                    이름:
                    <input type="text" value={value} onChange={handleChange} />
                </label>
                <button type="submit">제출</button>
            </form>
        )
    }
    ```
    
- HTML: 엘리먼트 내부에 각각의 state가 존재
    ```jsx
    <form>
        <label>
            이름:
            <input type="text" name="name" />
        </label>
        <button type="submit">제출</button>
    </form>
    ```
    

### Controlled Components

- 사용자가 입력한 값에 접근하고 제어할 수 있도록 해 주는 컴포넌트
- 값이 리액트의 통제를 받는 Input Form Element
- 사용자의 입력을 직접적으로 제어할 수 있음
- 여러 개의 입력 양식의 값을 원하는 대로 조정 가능 → 입력 양식의 초기값을 내가 원하는 대로 넣어 줄 수 있고 → 하나가 변경 되었을 때 다른 하나를 자동으로 변경할 수도 있음
- 예시 코드: 모든 입력값을 대문자로 변경하려면?
    ```jsx
    const handleChange = (eveent) => {
        setValue(eveent.target.value.toUpperCase())
    }
    ```
    

### 다양한 종류의 Forms
1. Textarea
    - 여러 줄에 걸쳐 긴 텍스트를 입력받기 위한 html 태그
    - 예시 코드
        ```jsx
        import { useState } from "react";
        
        function RequestForm(props) {
            const [value, setValue] = useState('요청사항을 입력하세요.')
        
            const handleChange = (event) => {
                setValue(event.target.value)
            }
        
            const handleSubmit = (event) => {
                alert('입력한 요청사항: ' + value);
                event.preventDefault();
              }
        
            return (
              <form onSubmit={handleSubmit}>
                <label>
                  요청사항
                  <textarea value={value} onChange={handleChange} />
                </label>
                <button type="submit">제출</button>
              </form>
            );
        }
        ```
        
2. Select
    - 드롭다운 목록을 보여주기 위한 html 태그
    - 예시 코드
        ```jsx
        import { useState } from "react";
        
        function FruitSelect(props) {
            const [value, setValue] = useState('grape')
        
            const handleChange = (event) => {
                setValue(event.target.value)
            }
            
            const handleSubmit = (event) => {
                alert('선택한 과일:' + value)
                event.preventDefault()
            }
        
            return (
                <form onSubmit={handleSubmit}>
                    <label>
                        과일을 선택하세요:
                        <select value={value} onChange={handleChange}>
                            <option value="grape">포도</option>
                            <option value="lime">라임</option>
                            <option value="coconut">코코넛</option>
                            <option value="mango">망고</option>
                        </select>
                    </label>
                    <button type="submit" value="Submit">제출</button>
                </form>
            )
        }
        ```
        - 포도라는 초기값을 가진 value가 하나 있음
        - 다중 선택을 하고 싶다면?
            ```jsx
            <select multiple={true} value={['B', 'C']}>
            ```
            
3. Input
    ```jsx
    <input type="text" value={value} onChange={handleChange} />
    ```
    

### 공통점
1. value라는 attribute를 사용해서 값을 전달
2. 값을 변경할 때는 onChange에서 setValue 함수를 사용해서 값을 업데이트

### File Input 태그
```jsx
<input type="file" />
```
- 디바이스의 저장 장치로부터 하나 또는 여러 개의 파일을 선택할 수 있게 해 주는 HTML 태그
- Uncontrolled Component: 읽기 전용 값이라 리액트의 동작을 받지 않음!

### Multiple Input
```jsx
function Resevation(props) {
    const [haveBreakfast, setHaveBreakfast] = useState(true)
    const [numberOfGuest, setNumberOfGuest] = useState(2)

    const handleSubmit = (event) => {
        alert(`아침식사 여부: ${haveBreakfast}, 방문객 수: ${numberOfGuest}`)
        event.preventDefault()
    }

    return (
        <form onSubmit={handleSubmit}>
          <label>
            아침식사 여부:
            <input
              type="checkbox"
              checked={haveBreakfast}
              onChange={(event) => {
                setHaveBreakfast(event.target.checked)
              }} />
          </label>
          <br />
          <label>
            방문객 수:
            <input
              type="number"
              value={numberOfGuests}
              onChange={(event) => {
                setNumberOfGuest(event.target.value)
              }} />
          </label>
          <button type="submit">제출</button>
        </form>
    );
}
```
- 다중 입력 제어
- 하나의 컴포넌트에서 여러 개의 입력을 다룰 경우?
- 여러 개의 state를 선언하여 각각의 입력에 대해 사용하면 가능

### Input Null Value
```jsx
// 입력 불가 상태
ReactDOM.render(<input value="hi" />, rootNode)

// 타이머에 의해 1초 뒤에 입력 가능한 상태로 변경
setTimeout(function() {
  ReactDOM.render(<input value={null} />, rootNode)
}, 1000) 
```
- value props을 정하면 코드를 수정하지 않는 한 사용자가 입력값을 바꿀 수 없음
- 만약 value props을 넣되 자유롭게 값을 바꾸게 하고 싶다면? → `undefined`나 `null`을 사용