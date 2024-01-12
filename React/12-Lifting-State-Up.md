# Lifting State Up

### Shared State
![Untitled](https://github.com/goldbutnew/TIL/assets/149566915/04a438d3-dbde-464a-a93d-2362ab41e9e2)
![Untitled 1](https://github.com/goldbutnew/TIL/assets/149566915/d6eee7b8-4953-4cc7-b62e-7a98b90252fb)
- 공유된 state
- 하나의 컴포넌트를 여러 개의 컴포넌트에서 표현해야 하는 경우
- 각각 보관하는 것이 아닌 가장 가까운 공통된 부모 컴포넌트의 state를 공유해서 사용
- 하위 컴포넌트가 공통된 부모 컴포넌트의 state를 공유하여 사용하는 것

### 하위 컴포넌트에서 state 공유하기

1. `BoilingVerdict`: 물의 끓음 여부를 알려주는 하위 컴포넌트 
    
    ```jsx
    function BoilingVerdict(props) {
      if (props.celsius >= 100) {
        return <p>The water would boil.</p>;
      }
      return <p>The water would not boil.</p>;
    }
    ```
    
2. `Calculator`: 부모 컴포넌트
    
    ```jsx
    function Calculator(props) {
        const [temperature, setTemperature] = useState('')
    
        const handleChange = (event) => {
            setTemperature(event.target.value)
        }
    
        return (
            <fieldset>
              <legend>Enter temperature in Celsius:</legend>
              <input
                value={temperature}
                onChange={handleChange} />
              <BoilingVerdict
                celsius={parseFloat(temperature)} />
            </fieldset>
        );
    }
    ```
    
    - BoilingVerdict 컴포넌트의 celsius라는 이름의 props로 전달됨
3. `TemperatureInput`: 입력 컴포넌트 추출하기
    ```jsx
    const scaleNames = {
        c: '섭씨',
        f: '화씨',
    }
    
    function TemperatureInput(props) {
        const [temperature, setTemperature] = useState('')
    
        const handleChange = (event) => {
            setTemperature(event.target.value)
        }
    
        return (
            <fieldset>
                <legend>
                    온도를 입력해 주세요(단위: {scaleNames[props.scale]})
                </legend>
                <input value={temperature} onChange={handleChange} />
            </fieldset>
        )
    }
    ```
    - 온도 입력하는 부분을 별도 컴포넌트로 추출
    - 섭씨 화씨를 각각 따로 입력받기
    - 재사용 가능한 컴포넌트 형태로 제작
4. `Calculator` 컴포넌트 변경
    ```jsx
    function Calculator(props) {
        return (
            <div>
                <TemperatureInput scale="c" />
                <TemperatureInput scale="f" />
            </div>
        )
    }
    ```
    - 여기서 문제: 사용자가 입력하는 온도값이 temperature input의 state에 저장되기 때문 섭씨 온도와 화씨 온도 값을 따로 입력 받으면 2개의 값이 다를 수가 있음! → 값을 동기화시켜 줘야 함
5. 온도 변환 함수 작성
    ```jsx
    function toCelsius(fahrenheit) {
        return ((fahrenheit - 32) * 5) / 9
    }
    
    function toFahrenheit(celsius) {
        return (celsius * 9) / 5 + 32
    }
    ```
6. `try-convert` 함수: 온도 값과 변환하는 함수를 파라미터로 받아서 값을 변환시켜 리턴해 주는 함수
    ```jsx
    function tryConvert(temperature, convert) {
        const input = parseFloat(temperature)
        if (Number.isNaN(input)) {
            return ''
        }
        const output = convert(input)
        const rounded = Math.round(output * 1000) / 1000
        return rounded.toString()
    }
    ```
    - 숫자가 아닌 값을 입력하면 empty 스트링을 입력하도록 예외처리
        ```jsx
        tryConvert('abc', toCelsius)        // empty string
        tryConvert('10.22', toFahrenheit)   // '50.396'을 리턴
        ```
7. `shared state` 적용하기
    - 컴포넌트를 상위 컴포넌트로 끌어올린다 → **Lifting State Up**
    - 하위 컴포넌트의 state를 공통 상위 컴포넌트로 끌어올린다
8. `TemperatureInput`의 죄종 완성본
    ```jsx
    const scaleNames = {
        c: '섭씨',
        f: '화씨',
    }
    
    // props와 scale과 temp 받아서 표시해 주며 온도값 변경
    function TemperatureInput(props) {
        const handleChange = (event) => {
            props.onTemperatureChange(event.target.value)
        }
    
        return (
            <fieldset>
                <legend>
                    온도를 입력해 주세요(단위: {scaleNames[props.scale]})
                </legend>
                <input value={props.temperature} onChange={handleChange} />
            </fieldset>
        )
    }
    
    export default TemperatureInput
    ```
    
    - state는 제거되었고 오로지 상위 컴포넌트에서 전달받은 값만을 사용
9. `Calculator` 최종 변경
    ```jsx
    import React, { useState } from "react"
    import TemperatureInput from "./TemperatureInput"
    
    function BoilingVerdict(props) {
        if (props.celsius >= 100) {
          return <p>The water would boil.</p>;
        }
        return <p>The water would not boil.</p>;
    }
    
    function toCelsius(fahrenheit) {
        return ((fahrenheit - 32) * 5) / 9
    }
    
    function toFahrenheit(celsius) {
        return (celsius * 9) / 5 + 32
    }
    
    function tryConvert(temperature, convert) {
        const input = parseFloat(temperature)
        if (Number.isNaN(input)) {
            return ''
        }
        const output = convert(input)
        const rounded = Math.round(output * 1000) / 1000
        return rounded.toString()
    }
    
    function Calculator(props) {
        const [temperature, setTemperature] = useState('')
        const [scale, setScale] = useState('c')
    
        const handleCelsiusChange = (temperature) => {
            setTemperature(temperature)
            setScale('c')
        }
    
        const handleFahrenheitChange = (temperature) => {
            setTemperature(temperature)
            setScale('c')
        }
    
        const celsius = scale === 'f' ? tryConvert(temperature, toCelsius) : temperature
        const fahrenheit = scale === 'c' ? tryConvert(temperature, toFahrenheit) : temperature
        
        return (
            <div>
                <TemperatureInput 
                    scale="c" 
                    temperature={celsius}
                    onTemperatureChange={handleCelsiusChange}
                />
                <TemperatureInput 
                    scale="f" 
                    temperature={fahrenheit}
                    onTemperatureChange={handleFahrenheitChange}
                />
                <BoilingVerdict
                    celsius={parseFloat(celsius)}
                />
            </div>
        )
    }
    
    export default Calculator
    ```
    
10. 최종 구조
    ![Untitled 2](https://github.com/goldbutnew/TIL/assets/149566915/148c7984-8a5b-4617-9eea-cd625115046f)