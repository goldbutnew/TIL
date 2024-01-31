## v-for
- 소스 데이터(Array, Object, number, string, Iterable)를 기반으로 요소 또는 템플릿 블록을 여러 번 렌더링

### v-for 구조
- v-for는 alias in expression 형식의 특수 구문을 사용하여 반복되는 현재 요소에 대한 별칭(alias)을 제공
    ```html
    <div v-for="(item, index) in myArr">
      {{ index }} // {{ item }}
    </div>
    ``` 
- 인덱스(객체에서는 키)에 대한 별칭을 지정할 수 있음
    ```html
    <div v-for="(value, key, index) in myObj">
      {{ index }} / {{ key }} / {{ value }}
    </div>
    ```

<br>

## v-for with key
- **반드시 v-for와 key를 함께 사용한다**
    - 내부 컴포넌트의 상태를 일관되게 유지
    - 데이터 예측 가능한 행동을 유지(Vue 내부 동작 관련)

### v-for와 key
- key는 반드시 각 요소에 대한 고유한 값을 나타낼 수 있는 식별자여야 함
    ```jsx
    let id = 0
    
    const items = ref([
      { id: id++, name: 'Alice' },
      { id: id++, name: 'Bella' },
    ])
    ```
    ```html
    <!-- Maintaining State with key -->
    <div v-for="item in items" :key="item.id">
      <!-- content -->
      {{ item }}
    </div>
    ```
    
<br>

## v-for with v-if
- **동일 요소에 v-for과 v-if를 함께 사용하지 않는다**
    - 동일한 요소에서 v-if가 v-for보다 우선순위가 더 높기 때문
    - v-if 조건은 v-for 범위의 변수에 접근할 수 없음

### v-for와 v-if 문제 상황
- todo 데이터 중 이미 처리한 (isComplete === true) todo만 출력하는 경우
    ```jsx
    const todos = ref([
      { id: id++, name: '복습', isComplete: true },
      { id: id++, name: '예습', isComplete: false },
      { id: id++, name: '저녁식사', isComplete: true },
      { id: id++, name: '노래방', isComplete: false }
    ])
    ```
    ```html
    <!-- [Bad] v-for with v-if -->
    <ul>
      <li v-for="todo in todos" v-if="!todo.isComplete" :key="todo.id">
        {{ todo.name }}
      </li>
    </ul>
    ``` 
    - TypeError: Cannot read properties of undefined (reading ‘isComplete’)
        - v-if가 더 높은 우선순위를 가지므로 v-for의 todo 요소를 v-if에서 사용할 수 없음

### v-for과 v-if 문제 상황 해결하기
1. **computed를 활용해 필터링 된 목록을 반환**하여 반복하도록 설정
    ```jsx
    const completeTodos = computed(() => {
      return todos.value.filter((todo) => !todo.isComplete)
    })
    ```
    ```html
    <!-- [Good] v-for with v-if & computed-->
    <ul>
      <li v-for="todo in completeTodos" :key="todo.id">
        {{ todo.name }}
      </li>
    </ul>
    ```    
2. v-for와 template 요소를 사용하여 **v-if를 이동**
    ```html
    <!-- [Good] v-for with v-if & template-->
    <ul>
      <template v-for="todo in todos" :key="todo.id">
        <li v-if="!todo.isComplete">
          {{ todo.name }}
        </li>
      </template>
    </ul>
    ```