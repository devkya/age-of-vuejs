# Vue.js 시작하기 - Age of Vue.js

Start date : 2022-09-17  
End date(예정) : 2022-09-30

## Vue 소개

- MVVM 패턴의 뷰모델 레이어에 해당하는 화면단 라이브러리
- Object.defineProperty() - [문서 링크](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)
  - vue-way.html 에서 사용법 확인 가능
    -IIFE(Immediately Invoked Funcion Expression) 즉시 실행 함수 표현 - 함수를 정의하고 바로 실행하여 변수에 함수를 저장하는 실행과정을 생략함. 정의하자마자 바로 호출함

```JavaScript
(funcion() {
    statements
}) ();
```

- vue API
  - 인스턴스에서 사용할 수 있는 속성(dictionary 형태)

```JavaScript
new Vue({
    el : ,
    template : ,
    data : ,
    methods : ,
    created : ,
    watch : ,
});
```

## Component

![Vue_component](https://vuejs.org/assets/components.7fbb3771.png)

- 화면의 영역을 구분하여 개발할 수 있는 뷰의 기능 -> 재사용성이 올라감

### Component Comunication

![Component_comunication](https://joshua1988.github.io/vue-camp/assets/img/component-communication.2bb1d838.png)

- N방향 통신에서는 데이터의 흐름을 파악하기 어려움
- 컴포넌트 통신 방식의 규칙이 생겼을 때 흐름을 파악하기 쉬움
- props vs event(emit)

### 같은 레벨에서 컴포넌트 통신 방법

- child component -> root component로 event 전달
- root component data 할당
- 전달하고자 하는 하위 컴포넌트 props로 전달

## Router

- vue.js 에서 페이지 간 이동을 위한 라이브러리
- 페이지 이동할 때 url이 변경되면 변경된 요소의 영역에서 컴포넌트를 갱신
  - SPA특징
  - DOM을 새로 갱신하는 것은 아님

`<router-view>`

- 페이지 표시 태그
- url에 따른 컴포넌트가 화면에 그려지는 영역

`<router-link to="path">`

- 컴파일 시, a tag로 변환
- to 속성
  - to 속성 값의 경로로 이동
  - v-bind와 함께 사용하면 동적으로 경로를 만들 수 있음
  - to="main/path" => current url에 path가 붙음
  - to="/main/detail" => default url에 path가 붙음
