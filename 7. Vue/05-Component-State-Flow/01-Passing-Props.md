# Passing Props

## 개요

- 부모는 자식에게 데이터를 전달(Pass Props)하며, 자식은 자신에게 일어난 일을 부모에게 알림(Emit event)
  ![Untitled](https://github.com/goldbutnew/TIL/assets/149566915/d8c6b1a5-ec28-43dc-849f-15afd0668db5)
      

### Props

- 부모 컴포넌트로부터 자식 컴포넌트로 데이터를 전달하는데 사용되는 속성

### One-Way-Data-Flow

- 모든 props는 자식 속성과 부모 속성 사이에 하향식 단방향 바인딩을 형성(one-way-down binding)

### Props 특징

- 부모 속성이 업데이트 되면 자식으로 흐르지만 그 반대는 안 됨
- 즉, 자식 컴포넌트 내부에서 props를 변경하려고 시도해서는 안 되며 불가능
- 또한 부모 컴포넌트가 업데이트 될 때마다 자식 컴포넌트의 모든 props가 최신값으로 업데이트
- **부모 컴포넌트에서만 변경**하고 **이를 내려받는 자식 컴포넌트**는 자연스럽게 갱신

### 단방향인 이유?

- 하위 컴포넌트가 실수로 상위 컴포넌트의 상태를 변경하여 앱에어스이 데이터 흐름을 이해하기 어렵게 만드는 것을 방지하기 위함

## Props 선언

- 부모 컴포넌트에서 보낸 props를 사용하기 위해서는 자식 컴포넌트에서 명시적인 props 선언이 필요

### Props 작성

- 부모 컴포넌트 Parent에서 자식 컴포넌트 ParentChild에 보낼 props 작성
    
    ```html
    <!-- Parent.vue -->
    
    <template>
      <div>
        <ParentChild **my-msg="message"** />
      </div>
    </template>
    ```
    
- **my-msg**=”**message**” / **(pop이름)**= “**(prop값)**”

### 1. 문자열 배열을 사용한 선언

```html
<!-- ParentChild.vue -->

<script setup>
  // 1. 문자열 배열 선언 방식
  defineProps(['myMsg'])
</script>
```

- `defineProps()`를 사용하여 props를 선언

### 2. 객체를 사용한 선언

```jsx
<!-- ParentChild.vue -->

<script setup>
	// 2. 객체 선언 방식
  defineProps({
  myMsg: {
      type: String,
      required: true,
    }
  })
</script>
```

- 객체 선언 문법의 각 객체 속성의 키는 props의 이름이 되며, 객체 속성의 값은 값이 될 데이터의 타입에 해당하는 생성자 함수(Number, String…)여야 함
- 객체 선언 문법 사용 권장

### prop 데이터 사용

- 템플릿에서 반응형 변수와 같은 방식으로 활용
    
    ```html
    <!-- ParentChild.vue -->
    
    <template>
      <div>
        <p>{{ myMsg }}</p>
    	</div>
    </template>
    ```
    
- props를 객체로 반환하므로 필요한 경우 JS에서 접근 가능
    
    ```jsx
    // props 데이터를 script에서 사용하려면
    const props = defineProps({
      myMsg: String,
    })
    
    console.log(props)
    console.log(props.myMsg)
    ```
    
- prop 출력 결과 확인
    
    ![Untitled 1](https://github.com/goldbutnew/TIL/assets/149566915/ea3552f5-714e-4932-a926-c376059ff0e2)
    

### 한 단계 더 prop 내려 보내기

1. ParentChild 컴포넌트를 부모로 갖는 ParentGrandChild 컴포넌트 생성 및 등록
    
    ```html
    <!-- ParentGrandChild.vue -->
    
    <template>
      <div>
      </div>
    </template>
    
    <script setup>
    </script>
    ```
    
    ```html
    <!-- ParentChild.vue -->
    
    <template>
      <div>
        <p>{{ myMsg }}</p>
        <ParentGrandChild />
      </div>
    </template>
    
    <script setup>
      import ParentGrandChild from '@/components/ParentGrandChild.vue';
    
      // 객체를 사용해 props 선언
      defineProps({
        myMsg: String,
      })
    </script>
    ```
    
2. ParentChild 컴포넌트에서 Parent로부터 내려받은 prop인 myMsg를 ParentGrandChild에게 전달
    
    ```html
    <!-- ParentChild.vue -->
    
    <template>
      <div>
        <p>{{ myMsg }}</p>
        <ParentGrandChild :my-msg="myMsg" />
      </div>
    </template>
    
    ```
    
    - v-bind를 사용한 동적 props
      
      ```html
      <!-- ParentGrandChild.vue -->
      
      <template>
        <div>
          <p>{{ myMsg }}</p>
        </div>
      </template>
      
      <script setup>
        defineProps({
          myMsg: String,
        })
      </script>
      ```
    
3. 출력 결과 확인
    
    ![Untitled 2](https://github.com/goldbutnew/TIL/assets/149566915/fdf3c7bc-4f2f-4095-9cdc-5988446e4b7b)
    
    - ParentGrandChild가 받아서 출력하는 prop은 Parent에 정의되어 있는 prop이며 Parent가 prop을 변경할 경우 이를 전달받고 있는 ParentChild, ParentGrandChild에서도 모두 업데이트 됨.

## Props 세부사항

### Props Name Casing

- 선언 및 템플릿 참조 시 (→ camelCase)
    
    ```html
    <p>{{ myMsg }}</p>
    ```
    
    ```html
    defineProps({
    	myMsg: String,
    })
    ```
    
- 자식 컴포넌트로 전달 시 (→ kebab-case)
    
    ```html
    <ParentChild my-msg="message" />
    ```
    
    - 기술적으로 camelCase도 가능하나 HTML 속성 표기법과 동일하게 kebab-case로 표기할 것을 권장

### Static props & Dynamic props

- 지금까지 작성한 것은 Static(정적) props
- v-bind를 사용하여 **동적으로 할당된 props**를 사용할 수 있음

---

1. Dynamic props 정의
    
    ```html
    <!-- Parent.vue -->
    
    <script setup>
    	import { ref } form 'vue'
    	
    	const name = ref('Alice')
    </script>
    ```
    
    ```html
    <!-- Parent.vue -->
    
    <ParentChild my-msg="message" :dynamic-props="name" />
    ```
    
2. Dynamic props 선언 및 출력
    
    ```html
    <!-- ParentChild.vue -->
    
    <script setup>
    	defineProps({
    		myMsg: String,
    		dynamicProps: String,
    	})
    </script>
    ```
    
    ```html
    <!-- ParentChild.vue -->
    
    <p>{{ dynamicProps }}</p>
    ```
    
3. Dynamic props 출력 확인
    
    ![Untitled 3](https://github.com/goldbutnew/TIL/assets/149566915/09a2fd39-cb37-46cc-92e2-2000901f7277)