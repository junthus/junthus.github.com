---
title: Vue.js
date: 2018-01-15 16:37:00
category:
- JavaScript
- Vue.js
---

[JS 프레임워크 백년전쟁에 결론이 날 때가 되었다](https://www.sitepen.com/blog/2017/11/10/web-frameworks-conclusions/)~~라고 하는데 사실 모르겠다~~

# HELLO WORLD 로 슥 훑어보는 삼대천왕
Q: `<div>Hello from ${framework}</div>` 찍기

## react
(사실 안써봐서 카더라 통신임)

```html
<!DOCTYPE html>
<html>
    <head>
        <title>React Hello World</title>
        <script src="https://fb.me/react-15.0.0.js"></script>
        <script src="https://fb.me/react-dom-15.0.0.js"></script>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.34/browser.min.js"></script>
   </head>
   <body>
       <div id="greeting"></div>
       <script type="text/babel">
           var Greeting = React.createClass({
               render: function() {
                   return (
                      <p>Hello from React</p> // p 태그 필요한건가...? 이것조차 모름. 날 믿지 말아여...
                   )
               }
           });
           ReactDOM.render(
                <Greeting/>,
                 document.getElementById('greeting')
           );
       </script>
   </body>
</html>
```

.| react
---|---
origin | 페북
good | 구조 단순, 유저수 많음 = 물어볼 데 많음 = 써드파티 많음 = 신기능 빨리나옴
bad | 코어가 단순한 만큼 추가 솔루션이 많이 필요하고 또 많이 제공 되어 있다지만<br>**검증되지 않은** 써드파티가 많음 = lib 구성할때 더듬더듬 모르모트화

## ang 투쁠
~~물론 요즘같은 세상에 cdn 파일 끌어다가 쓰겠단 건 아니지만 한 파일로 표현조차 못하겠음~~
```html
<!-- index.html -->
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Angular Hello World</title>
  <base href="/">

  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="icon" type="image/x-icon" href="favicon.ico">
</head>
<body>
  <app-root></app-root>
</body>
</html>
```
```js
// app.module.ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

```html
<!-- app.component.html -->
<div style="text-align:center">
Hello from {{what}}
</div>
```

```js
// app.components.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  what = 'Angular';
}
```

.| ang 2+
---|---
origin | 구글
good | 손에 익으면 생산성은 좋음, 머테리얼 디자인 적용 쉬움
bad | ts + reactiveJS 까지 사실상 같이 봐야 함 + 지들만의 세상을 한참 공부하도록 시킴<br>손에 익기까지 오래걸리고 파일 갯수 무한 증식하며 디버깅이 무슨 암호해독처럼 느껴짐 = 유지보수 자신없음<br>장점만 발라내어 레거시에 붙이기 불가능 = 프레임워크 적용하려고 하면 mkdir 부터 시작해야함<br>~~되니가 좋아하기 때문에 시름.~~

## vue.js 
```html
<!DOCTYPE html>
<html>
<head>
    <title>Vue Hello World</title>
    <script src="https://vuejs.org/js/vue.min.js"></script>
</head>
<body>
    <div id="app">
        {{ message }}
    </div>
     <script>
         new Vue({
              el: '#app',
              data: {
                  message: 'Hello from Vue'
                }
         });
         </script>
</body>
</html>
```
.| vue.js
---|---
origin | 대륙의 개발자
good | 단순. 검증 완료된 추가기능 솔루션들. 프레임워크의 적용 범위를 개발자가 결정 가능. 문서 짱.
bad | 리액트에 비하면 사용자 쫌 적은거 같다 ?
risk | (사실상) 1인 개발 체제 - 댓글 알바라도 풀었는지 이런 의견 종종 보이던데 이게 모 큰 흠인가 싶긴 함

<hr><hr><hr>

# vue.js의 Getting started를 읽고 돌아온 탕자
[설치+실행 대화형 CLI](https://kr.vuejs.org/v2/guide/installation.html#CLI)를 제공하고 더 설명할 거리가 없게 문서가 잘 되어 있다. 문서보세요 두 번 보세요.

> 다른 단일형 프레임워크와 달리 Vue는 점진적으로 채택할 수 있도록 설계하였습니다.

뷰의 **코어**는 발음 그대로 뷰에만 관여 -> 다른 라이브러리 생각 않고 레거시에 붙이기 가능하다니 포부 소박하고 쿨해...
[매력발산](https://kr.vuejs.org/v2/guide/comparison.html) 열심이라 귀엽고 [공식 라이브러리도 많고](https://github.com/vuejs/awesome-vue#components--libraries)... 그리고 이 모든것보다 우선해서, [**문서가 쩔게 잘 되어 있다**](https://kr.vuejs.org/v2/guide/).

## 특징들 : REACTIVE, DIRECTIVE, COMPONENT-IVE 

```html
<div id="app">
  <span v-bind:title="message">
    span.title attr에 app.message를 'keep' 바인딩
  </span>
</div>
```
```js
var app = new Vue({
  el: '#app',
  data: {
    message: 'Hi Again!'
  }
})
```

### 1. '선언적' 렌더링 - 데이터와 DOM은 REACTIVE
* [문서에 live 예제가 있음 멋짐](https://kr.vuejs.org/v2/guide/index.html#%EC%84%A0%EC%96%B8%EC%A0%81-%EB%A0%8C%EB%8D%94%EB%A7%81)

### 2. v- DIRECTIVE : 렌더링된 돔에 특수한 반응형 동작을 지시함
* `v-bind:(prop)`
* `v-if=(조건구문)`, `v-for="(반복구문)"` - 텍스트, 속성 뿐 아니라 DOM 구조에도 데이터 바인딩 가능
* `v-on:(eventName)` - 이벤트 리스너 선언 가능
* `v-model="(prop)"` - 양방향 바인딩 가능
  

### 3. COMPONENT

1.이런 뷰 인스턴스가 존재한다면 이것의 데이터를
```js
var component = new Vue({
  el: '#app',
  data: {
    groceryList: [
      { id: 0, text: 'Vegetables' },
      { id: 1, text: 'Cheese' },
      { id: 2, text: 'Whatever else humans are supposed to eat' }
    ]
  }
})
```
2.이렇게 정의된 컴포넌트를 이용해서

```js
Vue.component('todo-item', {
  props: ['todo'], // todo 변수로 데이터 들어올거야
  template: '<li>{{ todo.text }}</li>' // 그럼 <todo-item></todo-item>을 이렇게 치환해
})
```

* `props` option: 너와 나의 연결 고리
  * 상위 영역에서 테이터를 전달할 키 = 부모 영역의 데이터를 자식 컴포넌트에 내려줄 수 있음

3.요렇게 렌더링 할 수 있다.
```html
<div id="app">
  <ol>
    <todo-item
      v-for="item in groceryList"
      v-bind:todo="item"> // item 데이터를 todo 라는 키로 전달 받음
    </todo-item>
  </ol>
</div>
```
설명을 위해 순서를 바꿨지만 실제 코딩은 이것의 거의 역순으로. ([본문 예제보기](https://kr.vuejs.org/v2/guide/index.html#%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%9C-%EC%9E%91%EC%84%B1%EB%B0%A9%EB%B2%95))

<hr><hr>
# 여기부터 Essentials
공식문서와 이곳을 뛰어다니며 설명하니 어지러움 주의
<hr><hr>

# vue instance
일단 이렇게 루트 인스턴스를 만듬다
```js
var vm = new Vue({
  // 데이터, 템플릿, 마운트할 엘리먼트, 메소드, 라이프사이클 콜백 등의 옵션 props
})
```
* 우리 [mvvm](https://magi82.github.io/images/2017-2-24-android-mvc-mvp-mvvm/mvvm.png) 조금 비슷한거 같으니 알아두고...
* 컴포넌트들을 사용하다보면 이런 트리구조 어플리케이션을 만들 수 있슴.
```
Root Instance
└─ TodoList
   ├─ TodoItem
   │  ├─ DeleteTodoButton
   │  └─ EditTodoButton
   └─ TodoListFooter
      ├─ ClearTodosButton
      └─ TodoListStatistics
```
* 일단은 뷰 컴포넌트도 뷰 인스턴스라는 것만 알고 넘어가자 (물론 루트 인스턴스 특화 옵션이 있긴 함)
* 컴포넌트 시스템 나중에 또 얘기할거니까 넘어가 넘어가

## constructor option: `data` 
생성자 내에서 `data` 옵션에 할당될 때, 오브젝트 내에 미리 정의된 property는 반응형. [본문 참고](https://kr.vuejs.org/v2/guide/instance.html#%EC%86%8D%EC%84%B1%EA%B3%BC-%EB%A9%94%EC%86%8C%EB%93%9C)
* 그러니 나중에 필요한 prop은 초기값으로 미리 셋팅해야 하고
* 이걸 굳이 막아야 하는 상황이라면 `Object.freeze()`를 사용하라구 ~ 
  
## instance methods: `$` prefix
![vue_instance_methods](/images/vue_instance_methods.png)
* `vm.a = vm.$data.a`

## constructor options: instance lifecycle hooks 
![vue instace lifecycle](https://kr.vuejs.org/images/lifecycle.png)

<hr><hr><hr>

# 템플릿 문법 

Vue는 템플릿을 virtual DOM 렌더링 함수를 이용해서 컴파일
반응형 시스템: 상태 변경 추적 -> virtual DOM DIFF를 이용하여 최소한의 rendered DOM을 조작하도록 함.

* 문자열 및 표현식 = [\{ \{ mustache \} \}](https://mustache.github.io/)
* [디렉티브](https://kr.vuejs.org/v2/guide/syntax.html#%EB%94%94%EB%A0%89%ED%8B%B0%EB%B8%8C)
  * `v-${name}="단일 JS 표현식"`
  * `v-${name}:${args}`
  * `v-${name}:${args}.${modifiers}`
* shorthand
  * `v-bind:` -> `:`
  * `v-on:` -> `@`

<hr><hr><hr>

# Computed prop getter(setter도 있음)와 Watch 기능
[본문](https://kr.vuejs.org/v2/guide/computed.html#%EA%B3%84%EC%82%B0%EB%90%9C-%EC%BA%90%EC%8B%B1-vs-%EB%A9%94%EC%86%8C%EB%93%9C)

## constructor options: `computed`, `methods`

템플릿에 로직 넣지 말고 `computed` 쓰세여
* `computed`는 의존성 변경이 없는한 캐시됨
  * message 변수 값을 뒤집은 reversedMessage(computed값) 의 경우, message 값이 변하기 전까지 캐싱 

그러므로 캐싱을 원하지 않는 경우, `methods` 쓰고 표현식에서 호출하세여.
* `methods`는 재 렌더링 타임 마다 호출됨.

## constructor option: `watch`
`data` 옵션의 특정 프로퍼티를 감시할 수 있는 기능 - 남용 노노
하지만 양방향바인딩 같은 데이터는 `watch` prop을 걸어두면 편하겠죠 ?
* `vm.$watch`


<hr><hr><hr>

# `v-bind`: 클래스, 스타일 디렉티브
이거 많이 쓸텐데... 문자열 처리를 각각 해주려면 귀찮겠죠 ? 매-직 제공해 드립니다.

## 클래스 바인딩
* 객체 지원: `:class="{active: isActive}"`
  * 바인딩 된 객체는 위처럼 인라인일 수도, `data` prop에 정의된 객체일수도, `computed` 객체일수도.
* 배열 지원: `:class="[activeClass, errorClass]"`
* 혼용 지원: `:class="[{active: isActive}, errorClass]"` = 삼항연산
  
이 문법은 컴포넌트에도 동일하게 적용.
된다고 하는데 컴포넌트 아는게 없어서 설명을 못하고 넘어감...

## 스타일 바인딩
* 객체 지원: `:style="{fontSize: fontSize + 'px'}"`
  * 속성 이름에 camelCase, [kebab-case](http://wiki.c2.com/?KebabCase) 둘 다 사용 가능
* 배열 지원: `:style="[baseStyles, overridingStyles]"`
* 벤더 프리픽스 자동 (이라는데 재현을 못해봄)
  * 추가 loader를 써야 하나 ?
* 폴백 시스템 제공: `:style="{ display: ['-webkit-box', '-ms-flexbox', 'flex'] }"`

의문 : 컴파일 시점에 브라우저 정보를 알고 있진 않을텐데, 그럼 뷰는 런타임에 이것저것 챙겨 보고 업데이트를 시키는건가 ?

<hr><hr><hr>
# 조건부 렌더링
뷰는 진짜 깨끗하단 느낌이 드는게 조건에 안 맞으면 아예 그리지를 않는다. (button.disable 처럼)

[본문](https://kr.vuejs.org/v2/guide/conditional.html)

* `v-if` `v-else` `v-else-if`
  * `<template>` - target block : 토글 그룹
    * 가능한 한 렌더링을 줄이려고 하기 때문에 토글그룹끼리 겹치는 요소들이 다시 렌더링 되지 않는 문제가 생길 수 있음 - `key` attr 사용   
  * 마크업에서 실제 노드를 조작
* `v-show`- display:none 추가/제거


<hr><hr><hr>
# 리스트 렌더링
## v-for
* `v-for="itm in array"`
  * `v-for="(itm, idx) in array"`
  * `v-for="(val, key, idx) in obj"` - 내부적으로 `Object.keys()` 사용
  * `in` = `of`
* `v-bind:key`
  * 가능한 한 dom 을 건드리지 않으려고 하는 정책이기 때문에, 위의 조건부 렌더링에서 `key` attr 처럼 다시 렌더링(리스트의 경우엔 재정렬)해야 한다는 힌트를 제공해야 한다. 고유한 id를 사용하는 것이 일반적.
  * 이 구문은 vue가 노드를 식별하는 방법이기 때문에 `v-for`와 상관없는 다른 노드에서도 사용가능.
* `v-for="itm in 10"`
* `<template>` - target block : 반복 그룹
  
## priority: v-for > v-if
```html
<li v-for="todo in todos" v-if="!todo.isComplete">
  {{ todo }}
</li>
```
설명이 어려워서 그렇지 누가봐도 for 구문을 돌면서 if 조건을 체크해서 렌더링 하라는 것 같게 생김. ~~멋져~~

## 리스트용 데이터들 바인딩 - 이런 구멍 조심하세요
### 배열
* 배열 데이터를 래핑하여 추적 가능하게 제공하는데요
  * `push()` `pop()` `shift()` `unshift()` `splice()` `sort()` `reverse()`
  * 래핑되지 않은 방법으로 수정하면 감지 모태...
    * 래핑되지 않은 방법 == 배열에 인덱스로 접근해서 수정하거나 `length`를 변경하는 등
    * `Vue.set` 이나 `splice`를 활용하세요.
* non-mutating 하고 싶다면 - `filter()` `concat()` `slice()` 사용
  * 그렇다고 기존 DOM을 다 버리고 렌더링 하지는 않으니 걱정ㄴㄴ

### 객체
* vue instance 생성 시점에 선언이 안 되어 있었다면 바인딩도 안 되는데요
* `Vue.set(obj, key, val)`으로 동적 추가 가능합니다.
  * == `vm.$set`
* 혹은 기존의 obj를 확장해서 아래처럼 재할당 하시면 되여.

```js
this.userProfile = Object.assign({}, this.userProfile, {
  age: 27,
  favoriteColor: 'Vue Green'
})
```

## v-for와 컴포넌트 같이 쓸 수 있는데요
```html
<my-component 
  v-for="item in items" // 이 item 변수를 컴포넌트 영역..에 자동으로 주입하지는 않고
  v-bind:item="item" // 이렇게 prop을 이용해서 명시적으로 넣어 주어야 해요.
  v-bind:index="index"
  :key="item.id" // 이것도 꼭 챙겨주세요 (v2.2~)
></my-component>
```

# 끊으며
여기까지 문서를 읽으며 한 세 번 정도 컴포넌트 부분 읽고 올까... 하는 지점이 있었는데
문서님이 모르면 일단 넘어가라고 용서해주셔가지그
결국 읽어보지 못하고 준비해가지그

그래가지그여...

다음 타자님께 컴포넌트 잘 부탁드리면서
Essentials > 이벤트 핸들링 부터 시작하시면 된다는 토스.

그리고 아직까지 .vue 포맷이나 개발 포맷이 언급되지 않아서 
어떻게 소스(혹은 파일)를 구성해야 하는지 모르겠는데
언젠가 발표하실 분 화이팅 !

<hr><hr><hr>

# (부록)
MVC MVP MVVM... 패턴은 왜 쓰냐에 대한 한문장 정리 맘에 들어서.

> 화면에 보여주는 로직과 실제 데이터 처리 로직을 분리

* [MVC, MVP, MVVM 비교](https://magi82.github.io/android-mvc-mvp-mvvm/)


