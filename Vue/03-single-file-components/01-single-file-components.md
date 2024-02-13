## Component
- 재사용 가능한 코드 블록

### Component 특징
![Untitled](https://github.com/goldbutnew/TIL/assets/149566915/26138632-3042-46c2-aef8-a3fbbd8a5b77)
- UI를 독립적이고 재사용 가능한 일부분으로 분할하고 각 부분을 개별적으로 다룰 수 있음
- 그러면 자연스럽게 앱은 중첩된 Component의 트리로 구성됨

### Component 예시
![Untitled 1](https://github.com/goldbutnew/TIL/assets/149566915/48e6abc6-3c68-45b0-b4c9-9f168dd377e6)

<br>

## SFC
### Single-File Components(SFC)
- 컴포턴트의 탬플릿, 로직 및 스타일을 하나의 파일로 묶어낸 특수한 파일 형식 (`*.vue` 파일)

### SFC 파일 예시
- Vue SFC는 HTML, CSS 및 JS 3개를 합친 것
- `<template>`, `<script>` 및 `<style>` 블록은 하나의 파일에서 컴포넌트의 뷰, 로직 및 스타일을 캡슐화하고 배치

<br>

## SFC 문법

### SFC 문법 개요
- 각 *.vue 파일은 세 가지 유형의 최상위 언어 블록 `<template>`, `<script>`, `<style>`으로 구성됨
- 언어 블록의 작성 순서는 상관 없으나 일반 적으로 template → script → style 순서로 작성

### 언어 블록: `<template>`
- 각 *.vue 파일은 최상위 `<template>` 블록을 하나만 포함할 수 있음 (일반 `<script>` 제외)
- 컴포넌트의 `setup()` 함수로 사용되며 컴포넌트의 각 인스턴스에 대해 실행
```html
<template>
  <div class="greeting">{{  }}</div>
</template>
```

### 언어 블록: `<script setup>`
- *.vue 파일에는 하나의 **`<script setup>` 블록만 포함**할 수 있음 (일반 script 제외)
- 컴포넌트의 `setup()` 함수로 사용되며 컴포넌트의 각 인스턴스에 대해 설명
```html
<script setup>
import { ref } from 'vue'

const msg = ref('hello world!')
</script>
```

### 언어 블록: `<style scope>`
- *.vue 파일에는 **여러 `<style>` 태그**가 포함될 수 있음
- scoped가 지정되면 CSS는 현재 컴포넌트에만 적용
```html
<style scoped>
.greeting {
	color: red;
}
</style>

```

### 컴포넌트 사용하기
- Vue SFC는 컴파일러를 통해 컴파일 된 후 빌드 되어야 함
- 실제 프로젝트에서는 일반적으로 SFC 컴파일러를 Vite와 같은 공식 빌드 도구를 이용해 사용