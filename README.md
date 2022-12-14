# Vue.js 시작하기 - Age of Vue.js

Start date : 2022-09-17  
End date : 2022-09-21

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

## navigation guard

[링크](https://joshua1988.github.io/web-development/vuejs/vue-router-navigation-guards/)

뷰 라우터로 특정한 URL에 접근할 때 해당 URL의 접근을 막는 방법  
예를 들어, 사용자의 인증 정보가 없으면 특정 페이지에 접근하지 못하게 할 때 사용하는 기술

1. 애플리케이션 전역에서 동작하는 전역 가드
2. 특정 URL에서만 동작하는 라우터 가드
3. 라우터 컴포넌트 안에 정의하는 컴포넌트 가드

### 전역 가드

라우터 인스턴스를 참조하는 객체로 설정

```JavaScript
var router = new VueRouter();
// router 변수 아래에서 호출
router.beforeEach(function (to, from, next){
  // to : 이동할 url
  // from : 현재 url
  // next : to에서 지정한 url로 이동하기 위해 꼭 호출해야 하는 함수
  // 전역 가드를 설정하면 대기 상태가 됨 -> next() 호출로 이동
}
)
```

### 라우터 가드

```JavaScript
var router = new VueRouter({
  routes : [
    path : "/login",
    component : Login,
    beforeEnter : function(to, from, next){
      // 인증 값 검증 로직 추가
    }
  ]
})
```

### 컴포넌트 가드

```JavaScript
const Login = {
  template : '<p>Login Component</p>',
  beforeRouteEnter (to, from, next) {
    // login 컴포넌트가 화면에 표시되기 전에 수행될 로직
    // Login 컴포넌트는 아직 생성되지 않은 시점
  },
  beforeRouteUpdate (to, from, next) {
    // login 컴포넌트가 변경될 때 수행될 로직
    // this 로 Login 컴포넌트를 접근할 수 있음
  },
  beforeRouteLeave (to, from, next) {
    // login 컴포넌트를 화면에 표시한 url 값이 변경되기 직전의 로직
    // this 로 login 컴포넌트를 접근할 수 있음
  }
}
```

## Axios

[링크](https://github.com/axios/axios)

뷰에서 권고하는 HTTP 통신 라이브러리  
Promise 기반의 HTTP 통신 라이브러리이며 상대적으로 문서화 & API가 잘되어 있음  
async & await 비동기 처리 방법

- 궁금증

```javascript
// 1번 : .then 을 화살표 함수로 작성함
getData: function () {
            axios
              .get("https://jsonplaceholder.typicode.com/users")
              .then((res) => {
                console.log("GET() ... : ", res);
                this.users = res.data;
              })
              .catch(function (error) {
                console.log("ERR() ... : ", error);
              });
          }
```

```javascript
// 2번 : .then 을 function으로 작성함
getData: function () {
            axios
              .get("https://jsonplaceholder.typicode.com/users")
              .then(function (response) {
                console.log("GET() ... : ", res);
                this.users = res.data;
              })
              .catch(function (error) {
                console.log("ERR() ... : ", error);
              });
          },
```

arrow function을 사용했을 때는 data 할당이 잘 되지만 function을 사용했을 때는 data 할당이 되지 않음.

[arrow func vs func ](https://hhyemi.github.io/2021/06/09/arrow.html)
요약 : 화살표 함수와 일반 함수의 차이로 발생하는 문제로, 아래 코드를 이해하면 될듯함  
단, arrow function에서는 this 값을 변경할 수 없다 => 직접 확인해보기

```javascript
function fun() {
  this.name = "하이";
  return {
    name: "바이",
    speak: function () {
      console.log(this.name);
    },
  };
}

function arrFun() {
  this.name = "하이";
  return {
    name: "바이",
    speak: () => {
      console.log(this.name);
    },
  };
}

const fun1 = new fun();
fun1.speak(); // 바이

const fun2 = new arrFun();
fun2.speak(); // 하이
```

### async & await

[링크](https://joshua1988.github.io/web-development/javascript/js-async-await/)
JS의 비동기 처리 패턴 중 가장 최근에 나온 문법

```

```

## Watch vs Computed

[링크](https://vuejs.org/guide/essentials/computed.html#ad)

`computed` : 값을 계산  
`watch` : 부담스로운 로직, 데이터 요청에 적합함

## Event

### 이벤트 등록

브라우저가 이벤트 발생을 감지하는 방식 2가지

1. Event Bubbling

- 특정 화면 요소에서 이벤트가 발생했을 때 해당 이벤트가 더 상위의 화면 요소들로 전달되어 가는 특성을 의미

2. Event Capture

- 이벤트 번들링과 반대 방향으로 진행되는 이벤트 전파 방식
- `capture : true`

### event.stopPropagation()

- 상위 요소로 이벤트를 전달하는 것을 방해함

### event Delegation(이벤트 위임)

- 하위 요소에 각각 이벤트를 붙이지 않고 상위 요소에서 하위 요소의 이벤트들을 제어하는 방식
