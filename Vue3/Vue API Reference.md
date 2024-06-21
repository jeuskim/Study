- Vue 옵션 : Vue 컴포넌트의 동작과 특성을 정의

- template 옵션

  > 정의: 컴포넌트의 HTML 템플릿을 정의

- computed 옵션

  > 정의: data나 다른 속성이 변경될 때 함수가 한 번 실행해 캐싱된 값을 저장(동기식)
  >
  > 특징: 함수의 값을 리턴해야 한다.(동기식)

- watch 옵션

  > 정의: data나 다른 속성이 변경될 때 함수가 한 번 실행해 캐싱된 값을 저장
  >
  > 특징: 함수의 값을 리턴할 필요가 없다.(비동기식)
  >
  > 기본형: ```data또는속성명 ( 변경 후 data값, 변경 전 data값 ) { ... }```

- methods 옵션

  > 정의: Vue 인스턴스에서 사용할 함수를 등록하는 옵션

- data 옵션

  > 정의: 컴포넌트가 관리하고 추적해야 할 데이터

  - 디렉티브

    > 정의: 템플릿의 DOM 요소에 특별한 반응형 동작을 지정할 수 있도록 하는 특수한 속성

- props 옵션

- emits 옵션



# Vue API Reference

- update(갱신)

  > 정의: Vue 인스턴스의 데이터 ==> UI 담당하는 요소의 텍스트 컨텐츠

- element(요소)

  >  정의: HTML 문서 내의 DOM 요소
  >
  > 예: `<div>`, `<span>`, `<p>`

- text content(텍스트 컨텐츠)

  > 정의: element의 내부 텍스트
  >
  > 예: `<div>안녕하세요</div>`의 "안녕하세요"

## 1. Global API

#### 1.1 Aplication

#### 1.2 General

<hr />

## 2. Composition API

#### 2.1 setup()

#### 2.2 Reactivity: Core

#### 2.3 Reactivity: Utilities

#### 2.4 Reactivity: Advanced

#### 2.5 Lifecycle Hooks

#### 2.6 Dependency Injection

<hr />

## 3. Options API

#### 3.1 Options: State

- data
- props
- computed
- methods
- watch
- emits
- expose

#### 3.2 Options: Rendering

- template
- render
- compilerOptions
- slots

#### 3.3 Options: Lifecycle

- beforeCreate
- created
- beforeMount
- mounted
- beforeUpdate
- updated
- beforeUnmount
- unmounted
- errorCaptured
- renderTracked
- renderTriggered
- activated
- deactivated
- serverPrefetch

#### 3.4 Options: Composition

- provide
- inject
- mixins
- extends

#### 3.5 Options: Misc

#### Component Instance

<hr />

## 4. Built-ins

#### 4.1 Directives

- v-text

  - 정의: Update the element's text content.

    - update(갱신)

      > 정의: Vue 인스턴스의 데이터 ==> UI 담당하는 요소의 텍스트 콘텐츠

    - element(요소)

      >  정의: HTML 문서 내의 DOM 요소
    >
      > 예: `<div>`, `<span>`, `<p>`
  
    - text content(텍스트 콘텐츠)

      > 정의: element의 내부 텍스트
    >
      > 예: `<div>안녕하세요</div>`의 "안녕하세요"
  
  - 타입: string

  - 단방향 바인딩: Vue 인스턴스 데이터(ModelView) ==> 텍스트 콘텐츠(View)

  - 예:

    ```html
    <span v-text="msg"></span>
    <!-- same as -->
    <span>{{msg}}</span>
    ```

- v-html

  - 정의: Update the element's innerHTML.

    - innerHTML

      > 정의: element의 속성으로, 해당 element의 HTML content를 문자열 형태로 읽거나 설정

  - 타입: string

  - 단방향 바인딩: Vue 인스턴스 데이터(ModelView) ==> HTML 콘텐츠(View)

  - 예:
  
    ```html
    <div v-html="html"></div>
    ```

- v-show

  - 정의: Toggle the element's visibility based on the truthy-ness of the expression value.

    - toggle(전환하다)

      > 정의: element를 보이게 하거나 숨기는 상태로 변경하듯이 상태를 전환하는 것

    - truthy-ness

      > 정의: 자바스크립트에서 "참"으로 평가되는 값

    - expression value

      > 정의: 자바스크립트 표현식의 값

  - 타입: any

  - 특징: 렌더링을 수행한 후 화면에 보일지 숨길지 결정한다.

- v-if

  - 정의: Conditionally render an element or a template fragment based on the truthy-ness of the expression value.

    - render(렌더링하다)

      > 정의: element나 template을 실제로 DOM에 추가하여 화면에 표시하는 것

    - template fragment

      > 정의: Vue template 안에 정의된 여러 element들을 포함한 부분

  - 타입: any

- v-else

- v-else-if

  - 예:

    ```html
    <div v-if="type === 'A'">A</div>
    <div v-else-if="type === 'B'">B</div>
    <div v-else-if="type === 'C'">C</div>
    <div v-else>Not A/B/C</div>
    ```

- v-for

  - 정의: Render the element or template block multiple times based on the source data.

  - 타입: ```Array | Object | number | string | Iterable```

    - Iterable 객체 : `for...of` 루프를 사용하여 반복(iterate)할 수 있는 객체

  - 예:

    ```html
    <div v-for="item in items">{{ item.text }}</div>
    <div v-for="(item, index) in items"></div>
    <div v-for="(value, key) in object"></div>
    <div v-for="(value, name, index) in object"></div>
    ```

- v-on

  - 정의: Attach an event listener to the element.

    - attach(첨부하다)

      > 정의: 특정 event가 발생할 때 실행할 함수를 element에 연결

    - event(이벤트)

      > 정의: 사용자가 페이지와 상호 작용할 때 발생하는 것
      >
      > 예: `click`, `keydown`, `mouseover`, `submit`

    - event handler(이벤트 핸들러)

      > 정의: 특정 이벤트가 발생할 때 실행되는 함수

    - event listener(이벤트 리스너)

      > 정의: 이벤트를 감시하고 이벤트 핸들러를 호출

  - expects type: ```Function | Inline Statement | Object (without argument)```

    - 예: ```doThis | doThis('hello', $event) | { mousedown : doThis, mouseup : doThat }```

  - 단방향 바인딩: 이벤트 리스너(View) ==> Vue 인스턴스 메서드(Model View)

  - 인자: `event`

  - 식별자(modifiers)

    - .stop : call `event.stopPropagation()`.
    - .prevent : call `event.preventDefault()`.
    - .capture : add event listener in capture mode.
    - .self : only trigger handler if event was dispatched from this element.
    - .{keyAlias} : only trigger handler on certain keys.
    - .once : only trigger handler at most once.
    - .left : only trigger handler for left button mouse events.
    - .right : only trigger handler for right button mouse events.
    - .middle : only trigger handler for middle button mouse events.
    - .passive : attaches a DOM event with `{ passive: true }`.

  - 예:

    ```html
    <!-- method handler -->		<button v-on:click="doThis"></button>
    <!-- shorthand -->			<button @click="doThis"></button>
    <!-- View 역할을 하는 button HTML element의 attribute인 click event listener 로부터 	ViewModel 역할을 하는 Vue instance methods의 doThis function 에 바인딩 -->
    
    <!-- dynamic event -->
    <button @[event]="doThis"></button>
    <!-- View 역할을 하는 button HTML element의 사용자 attribute인 event(Vue instance data에 event:value 인 property 존재) event listener 로부터
    ViewModel 역할을 하는 Vue instance methods의 doThis function 에 바인딩 -->
    
    <!-- inline statement -->
    <button @click="doThat('hello', $event)"></button>
    <!-- View 역할을 하는 button HTML element의 attribute인 click event listener 로부터
    ViewModel 역할을 하는 Vue instance methods의 doThis function(첫 번째 인자로 'hello' 문자열, 두 번째 인자로 Javascript click event object를 가짐) 에 바인딩 -->
    
    <!-- object syntax -->
    <button v-on="{ mousedown: doThis, mouseup: doThat }"></button>
    <!-- View 역할을 하는 button HTML element의 attribute인 mousedown event listener 로부터 ViewModel 역학을 하는 Vue instance methods의 doThis function 에 바인딩하고
    View 역할을 하는 button HTML element의 attribute인 mouseup event listener 로부터
    ViewModel 역할을 하는 Vue instance methods의 doThat function 에 바인딩-->
    ```

- v-bind

  - 정의: Dynamically bind one or more attributes, or a component prop to an expression.

    - attributes(속성)

      > 정의: element의 속성

    - component prop

      > 정의: Vue component의 속성

  - expects type: `any (with argument) | Object (without argument)`

    - 예: ```imageSrc , [classA, classB] | { red: isRed }```

  - 단방향 바인딩: Vue 인스턴스 데이터(ModelView) ==> element의 attributes(View)

  - 인자: `attrOrProp (optional)`

  - 식별자(modifiers)

    - .camel : transform the kebab-case attribute name into camelCase.
    - .prop : force a binding to be set as a DOM property.
    - .attr : force a binding to be set as a DOM attribute.

  - 예:

    ```html
    <!-- bind an attribute -->		<img v-bind:src="imageSrc" />
    <!-- shorthand -->				<img :src="imageSrc" />
    	<!-- ViewModel 역할을 하는 Vue instance data(key가 imageSrc인 property) 로부터
    	View 역할을 하는 img DOM element의 attribute인 src 에 바인딩 -->
    
    <!-- dynamic attribute name -->	<button :[key]="value"></button>
    	<!-- ViewModel 역할을 하는 Vue instance data(key:value인 property) 로부터
    	View 역할을 하는 button DOM element의 사용자 attribute인 key 에 바인딩 -->
    
    <!-- same-name -->				<img :src />
    	<!-- ViewModel 역할을 하는 Vue instance data(key가 src인 property) 로부터
    	View 역할을 하는 img DOM element의 attribute인 src 에 바인딩 -->
    
    <!-- class binding -->
    <div :class="{ red: isRed }"></div>
    	<!-- ViewModel 역할을 하는 Vue instance data(key가 isRed인 property) 로부터
    	View 역할을 하는 div DOM element의 attribute인 red class 에 바인딩 -->
    <div :class="[classA, classB]"></div>
    	<!-- ViewModel 역할을 하는 Vue instance data(classA:클래스명1인 property) 로부터
    	View 역할을 하는 div DOM element의 attribute인 클래스명1 에 바인딩하고
    	ViewModel 역할을 하는 Vue instance data(classB:클래스명2 인 property) 로부터
    	View 역할을 하는 div DOM element의 attribute인 클래스명2 에 바인딩 -->
    <div :class="[classA, { classB: isB, classC: isC }]"></div>
    	<!-- ViewModel 역할을 하는 Vue instance data(classA:클래스명1인 property) 로부터
    	View 역할을 하는 div DOM element의 attribute인 클래스명1 에 바인딩하고
    	ViewModel 역할을 하는 Vue instance data(key가 isB인 property) 로부터
    	View 역할을 하는 div DOM element의 attribute인 classB class 에 바인딩하고
    	ViewModel 역할을 하는 Vue instance data(key가 isC인 property) 로부터
    	View 역할을 하는 div DOM element의 attribute인 classC class 에 바인딩 -->
    
    <!-- style binding -->
    <div :style="{ fontSize: size + 'px' }"></div>
    	<!-- ViewModel 역할을 하는 Vue instance data(key가 size인 property) 로부터
    	View 역할을 하는 div DOM element의 attribute인 style object(key가 fontSize인
    	property) 에 바인딩 -->
    <div :style="[styleObjectA, styleObjectB]"></div>
    	<!-- ViewModel 역할을 하는 Vue instance data(객체명이 styleObjectA) 로부터
    	View 역할을 하는 div DOM element의 attribute인 style object 에 바인딩하고
    	ViewModel 역할을 하는 Vue instance data(객체명이 styleObjectB) 로부터
    	View 역할을 하는 div DOM element의 attribute인 style object 에 바인딩 -->
    
    <!-- binding an object of attributes -->
    <div v-bind="{ id: someProp, 'other-attr': otherProp }"></div>
    	<!-- ViewModel 역할을 하는 Vue instance data(id:someProp 인 property) 로부터
    	View 역할을 하는 div DOM element의 attribute인 id 에 바인딩하고
    	ViewModel 역할을 하는 Vue instance data('other-attr':otherProp 인 property)
    	로부터 View 역할을 하는 div DOM element의 사용자 attribute인 other-attr 에 바인딩
    	-->
    
    <!-- prop binding -->			<MyComponent :prop="someThing" />
    	<!-- Vue instance data(key가 someThing인 property) or
    	Vue instance methods(함수명이 someThing) 로부터
    	child component(component명이 MyComponent)의 props option
    	(key가 prop인 property) 에 바인딩 -->
    <!-- pass down parent props -->	<MyComponent v-bind="$props" />
    <!-- XLink -->					<svg><a :xlink:special="foo"></a></svg>
    ```

- v-model

  - 정의: Create a two-way binding on a form input element or a component.
    - form(웹 폼)

      > 정의: 사용자가 데이터를 입력하고 제출할 수 있는 HTML 요소
      >
      > 예: `<input>`, `<select>`, `<textarea>`, `components`
    
  - 타입: form input element, component

  - 양방향 바인딩: Vue 인스턴스 데이터(ModelView) <==> element의 attributes(form의 event listener)

    > Vue 인스턴스 데이터(ModelView) ==> element의 attributes(View)
    >
    > element의 attributes(form input element의 event listener)(View)
    >
    > ==> Vue 인스턴스 메서드 ==> Vue 인스턴스 데이터(ModelView)

  - 식별자(modifiers)

    - .lazy : listen to `change` events instead of `input`
    - .number : cast valid input string to numbers
    - .trim : trim input

- v-slot

- v-pre

- v-once

- v-memo

- v-cloak

#### 4.2 Components

#### 4.3 Special Elements

#### 4.4 Special Attributes

<hr />

## 5. Single-File Component

#### 5.1 Syntax Specification

#### 5.2 \<script setup\>

#### 5.3 CSS Feature

<hr />

## 6. Advanced APIs

#### 6.1 Render Function

#### 6.2 Server-Side Rendering

#### 6.3 TypeScript Utility Types

#### 6.4 Custom Renderer

#### 6.5 Compile-Time Flags

<hr />

# 생명주기 메서드

- Vue instance 생성
- beforeCreate()
  - Vue instance 초기화
- created()
  - template parsing: 템플릿 문자열을 AST로 변환
    - 추상 구문 트리(Abstract Syntax Tree, AST)
  - AST compile: AST를 렌더링 함수로 컴파일
  - 가상 DOM rende: 렌더링 함수와 데이터 결합
- beforeMount()
  - Patching(가상 DOM과 실제 DOM 동기화)
- mounted()
  - 데이터 변경
- beforeUpdate()
  - 가상 DOM Re-rende(가상 DOM 재생성)
  - Patching(가상 DOM과 실제 DOM 동기화)
- updated()
  - 가상 DOM 제거
- beforeUnmount()
  - 가상 DOM 제거(최상위 컴포넌트 -> 최하위 컴포넌트)
  - 실제 DOM 제거(최하위 컴포넌트 -> 최상위 컴포넌트)
- unmounted()
