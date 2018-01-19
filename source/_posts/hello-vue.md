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
bad | 코어가 단순한 만큼 추가 솔루션이 많이 필요하고 또 많이 제공 되어 있다지만<br>**검증되지 않은** 써드파티가 많음 = lib 구성할때 더듬더듬

## ang 투쁠
~~물론 요즘같은 세상에 cdn 파일 끌어다가 쓰겠단 건 아니지만 한 파일로 표현조차 못하겠음~~ \+ 컴파일까지 해야 돌아감

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
  // styleUrls: ['./app.component.css'] // css가 필요할 경우 이런식으로.
})
export class AppComponent {
  what = 'Angular';
}
```

.| ang 2+
---|---
origin | 구글
good | 손에 익으면 생산성은 좋음, 머테리얼 디자인 적용 쉬움
bad | ts + RXJS 까지 사실상 같이 봐야 함 + 지들만의 세상을 한참 공부하도록 시킴<br>손에 익기까지 오래걸리고 파일 갯수가 무한 증식(컴포넌트*3)하며 뭐 선언만 하나 잘못되어도 콘솔에 에러로그가 100줄정도씩 떠서 디버깅이 무슨 암호해독처럼 느껴짐 = 유지보수는 내가 안 하겠다는 굳은 마음을 먹게 됨<br>장점만 발라내어 레거시에 붙이기 불가능 = 프레임워크 적용하려고 하면 mkdir 부터 시작해야함

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

<hr><hr>
**요약: 코드가 한 눈에 이해되고 구조가 단순하면서도 점진적 적용이 가능하다는 뷰를 써볼까요 ?**

준비물: [설치 + boilerplate CLI](https://kr.vuejs.org/v2/guide/installation.html#CLI) 
<hr><hr>

# vue.js의 Getting started를 읽고 주절주절

> 다른 단일형 프레임워크와 달리 Vue는 점진적으로 채택할 수 있도록 설계하였습니다.

뷰의 **코어**는 발음 그대로 뷰에만 관여 -> 다른 라이브러리 생각 않고 레거시에 붙이기 가능(포부 소박하고 쿨해...)
'누군가 알아서 나를 알아봐주겠지'하지 않고 [매력발산](https://kr.vuejs.org/v2/guide/comparison.html) 열심히 함
[공식 라이브러리](https://github.com/vuejs/awesome-vue#components--libraries)도 잘 준비해 둠

그리고 이 모든것보다 우선해서, [**가이드 문서가 쩔게 잘 되어 있다**](https://kr.vuejs.org/v2/guide/).

## vue 특징들 : REACTIVE, DIRECTIVE, COMPONENT-IVE 

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

### 1. '선언적' 렌더링 + REACTIVE(데이터 -> DOM)

선언형(declarative)은 명령형(imperative)이라는 말과 대치되는 단어.
우리가 기존에 `message`를 어떤 화면에 찍기 위해서는 이런 파편회된 조치들이 필요했다.
* 콘솔표시 -> console.log()
* 화면표시 -> innerHTML=""
* 출력 -> ...

특정 언어의 초기에는 이러한 조치들을 구구절절맨으로 개발자가 하나하나 처리해야 한다면(imperative)
일정 기간 그 언어에 대한 여러가지 폴백과 고민들이 이루어지고 나면
그 처리를 위임하는 시스템을 구축할 수 있고 그게 '선언적' 인 제스쳐로 나타난다.

그 예로, 선행된 '선언'의 역사에는 이런 것들이 있다.
* 마크업 언어
* css - `border-radius`

'반응형'이라는 의미도 이와 비슷한 맥락의 이야기인데,
뷰의 경우 바인딩된 모델의 데이터가 변경되는 경우 뷰의 값도 '계속' 변경된다.
이것도 예전에 이런식으로 구구절절 명령해 줘야 했다면
* 이벤트 탐지
* 이전의 값과 같은가? + validation
* 업데이트
* 실패하면

반응형은 마치 like excel 처럼, 그 중간 과정들을 생략하고
**원본 데이터 변경 = 결과도 변경**
이런 흐름으로 app을 개발할 수 있게 만들어 준다.

~~잘 정리 한 건지 모르겠다~~

### 2. `v-` DIRECTIVE : 렌더링된 돔에 특수한 반응형 동작을 지시함
* `v-bind:(prop)`
* `v-if=(조건구문)`, `v-for="(반복구문)"` : 텍스트, 속성 뿐 아니라 DOM 구조에도 데이터 바인딩 가능
* `v-on:(eventName)` : 이벤트 리스너 선언 가능
* `v-model="(prop)"` : 양방향 바인딩 가능

### 3. COMPONENT

1.데이터: 이런 데이터가 들어있는 뷰 인스턴스를
```js
var app = new Vue({
  el: '#app',
  data: {
    groceryList: [ // 이것을 사용할 예정
      { id: 0, text: 'Vegetables' },
      { id: 1, text: 'Cheese' },
      { id: 2, text: 'Whatever else humans are supposed to eat' }
    ]
  }
})
```
2.템플릿: 이렇게 정의된 컴포넌트를 이용해서

```js
Vue.component('todo-item', {
  props: ['todo'], // todo 변수로 부모님이 데이터 주실거야
  template: '<li>{{ todo.text }}</li>' // 그럼 <todo-item></todo-item>을 이걸로 치환해
})
```

* `props` option
  * vue component는 독립된 스코프를 가지게 되는데
  * 이 때 부모의 데이터를 자식 컴포넌트에게 전달해 주는 방법

3.사용: 요렇게 렌더링 할 수 있다.
```html
<div id="app">
  <ol>
    <todo-item
      v-for="item in groceryList"
      v-bind:todo="item"> <!-- item 데이터를 todo 라는 키로 전달 -->
    </todo-item>
  </ol>
</div>
```
설명을 위해 순서를 바꿨지만 실제 코딩은 이것의 거의 역순으로. ([본문 예제보기](https://kr.vuejs.org/v2/guide/index.html#%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%9C-%EC%9E%91%EC%84%B1%EB%B0%A9%EB%B2%95))

<hr><hr>
# 여기부터 Essentials
공식문서와 이곳을 뛰어다니며 설명하니 어지러움 주의
<hr><hr>

# vue 인스턴스에 관하여
일단 이렇게 루트 인스턴스를 만듬다. 뷰 인스턴스는 app 내에 일반적으로 하나가 존재함다.
```js
var vm = new Vue({
  // 데이터, 템플릿, 마운트할 엘리먼트, 메소드, 라이프사이클 콜백 등의 옵션 props
})
```
* 뷰 컴포넌트도 뷰 인스턴스라는 것만 알고 넘어가자 (물론 루트 인스턴스 특화 옵션이 있긴 함)
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
* 컴포넌트 시스템 나중에 또 얘기할거니까 넘어가 넘어가

## constructor option: `data` 
* 인스턴스 생성시 `data` 옵션 - 오브젝트 내에 미리 정의된 prop만 반응형으로 동작
  * (아마) [`Proxy`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Proxy) + [`Object.defineProperty`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)를 이용해서 객체의 변경을 탐지하는 듯 한데 
  `defineProperty`는 prop의 '선언'이나 '변경'만을 감지 할 수 있음. 
  ('추가' 는 감지가 안 됨, prop의 reference가 선언시에 참조되어야 하는 듯)
* 그러니 나중에 필요한 prop은 초기값으로 미리 넣어서 참조할 수 있도록 사용해야 함.
* 혹시 데이터 바인딩을 통째로 막아야 하는 상황에 대비해서 `Object.freeze()`제공
  
([혹-시 vue.js 구현 궁금하면](https://vuejs.org/js/vue.js) 열어서 `Object.defineProperty` 같은 것을 찾아보자.)

## instance methods: `$` prefix로 제공
`vm.a = vm.$data.a` 이런 alias 정도임
잘 안씀 = 안 중요함 = 지나가 지나가
![vue_instance_methods](/images/vue_instance_methods.png)

## constructor options: instance lifecycle hooks 
(이벤트가 아닌) 콜백으로 특정 타이밍의 동작을 수행 할 수 있음. (그림의 빨간 박스들)
![vue instance lifecycle & hooks](/images/vue-lifecyclehooks.png) 

* `beforeCreate` `created`
* `beforeMount` `mounted`
* `beforeUpdate` `updated`
* `activated` `deactivated`
* `beforeDestroy` `destroyed`
* `errorCaptured`

<hr><hr><hr>

# 템플릿 문법 

Vue는 템플릿을 virtual DOM 렌더링 함수를 이용해서 컴파일.

* 내부 반응형 시스템을 이용하여 상태 변경을 추적하고 그 데이터를 기반으로 virtual DOM DIFF를 이용하여 최소한의 rendered DOM을 조작하도록 함.
  * == 최소한의 rendered DOM 변경을 기본 정책으로 삼고 있음

## 문법들
* 문자열 및 표현식 = [\{ \{ mustache \} \}](https://mustache.github.io/)
* [디렉티브](https://kr.vuejs.org/v2/guide/syntax.html#%EB%94%94%EB%A0%89%ED%8B%B0%EB%B8%8C)
  * `v-${name}="단일 JS 표현식"`
  * `v-${name}:${args}`
  * `v-${name}:${args}.${modifiers}`
* shorthand
  * `v-bind:` -> `:`
  * `v-on:` -> `@`

<hr><hr><hr>

# vue의 Watch 기능
[본문이 더 이해하기 쉬움](https://kr.vuejs.org/v2/guide/computed.html)

## constructor option: `watch`
`data` 옵션의 특정 프로퍼티 감시 -> 뭔가를 변경할 때 프록시 기능 
= 기타 다른 프레임워크에서 제공하는 감시 기능과 유사

* `vm.$watch`와 동일
* 어떨 때 유용한가 : 데이터 바인딩의 흐름 사이에서 추가 작업이 필요한 경우 or 의도적으로 흐름에 딜레이를 주려는 경우
  * 다른 라이브러리(데이터 변경 시점에 트리거가 필요한)와 혼용하는 경우
  * debounce
* 양방향바인딩 같은 데이터는 걸어둘만 함

## constructor options: `computed`, `methods`

vue: `watch` 제공하긴 하는데 웬만한건 알아서 해 드릴게여~ (`data`)

그런데 기존 표현식들을 이용해서 템플릿 내에 구구절절 쓸 수 있긴 하지만 지저분하지요 ?
-> 템플릿에 로직 넣지 말고 `computed` 옵션을 쓰세여

* `computed`는 의존성 변경이 없는한 캐시됨
  * message 변수 값을 뒤집은 reversedMessage(computed값) 의 경우, message 값이 변하기 전까지 캐싱 
  * getter 의 `this.message`(원본데이터)의 참조를 저장, 변경시에 값 업데이트 = 캐싱이 가능하도록 함

혹시 캐싱을 원하지 않는 경우, `methods` 쓰고 표현식에서 호출하세여.
* `methods`는 재 렌더링 타임 마다 호출됨.

<hr><hr><hr>

# `v-bind`: 클래스, 스타일 디렉티브
이거 많이 쓸텐데... 문자열 처리를 각각 해주려면 귀찮겠죠 ? 매-직 제공해 드립니다.

[이것도 본문이 더 이해하기 쉬움](https://kr.vuejs.org/v2/guide/class-and-style.html)

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
뷰는 조건에 안 맞으면 아예 rendered DOM에 그리지를 않는다. 
(`<button disable=false></button>`를 `<button></button>`으로 깨끗하게 렌더링 하는 것 처럼)

[예제를 보면 이해하기 쉬움](https://kr.vuejs.org/v2/guide/conditional.html#key%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EC%9E%AC%EC%82%AC%EC%9A%A9-%EA%B0%80%EB%8A%A5%ED%95%9C-%EC%97%98%EB%A6%AC%EB%A8%BC%ED%8A%B8-%EC%A0%9C%EC%96%B4): 개발자 도구 열어놓고 돔 변경되는 것 확인하기.

* `v-if` `v-else` `v-else-if`
  * `<template>`: 렌더링 토글 대상그룹으로 사용할 수 있는 문법
    * 가능한 한 렌더링을 줄이려고 하기 때문에 토글그룹끼리 겹치는 요소들이 다시 렌더링 되지 않는 문제가 생길 수 있음 - `key` attr 사용   
  * 조건에 안 맞으면 아예 그리지 않음
  * 런타임에 이 조건이 변경되면 마크업에서 실제 노드를 조작(비용↑)
* `v-show`
  * 마크업에는 노드가 항상 존재하고 `display:none` 추가/제거


<hr><hr><hr>
# 리스트 렌더링
## v-for
* `v-for="itm in array"`
  * `v-for="(itm, idx) in array"`
  * `v-for="(val, key, idx) in obj"` - 내부적으로 `Object.keys()` 사용
  * `in` = `of`
* `v-bind:key`
  * 가능한 한 렌더링을 줄이려는 정책이기 때문에 DOM을 재사용하다보니 업데이트시 예상하지 않는 동작을 할 수 있듬
  * 위의 조건부 렌더링에서 `key` attr 처럼 다시 렌더링(리스트의 경우엔 재정렬)해야 한다는 힌트를 제공해야 함. key=고유한 id를 사용하는 것이 일반적.
  * 이 구문은 vue가 노드를 식별하는 방법이기 때문에 `v-for`와 상관없는 다른 노드에서도 사용가능.
* `v-for="itm in 10"`
* 이때 `<template>`: 반복 대상그룹으로 사용할 수 있는 문법.
  
## priority: v-for > v-if
== for 구문을 돌면서 if 조건을 체크해서 렌더링 함.
```html
<li v-for="todo in todos" v-if="!todo.isCompleted">
  {{ todo }}
</li>
```


## 리스트용 데이터들 바인딩 - 이런 구멍 피하세요
### 배열
* 배열 데이터를 래핑하여 추적 가능하게 제공하는데요
  * `push()` `pop()` `shift()` `unshift()` `splice()` `sort()` `reverse()`
  * 래핑되지 않은 방법으로 수정하면 감지 모태...
    * 래핑되지 않은 방법 == 배열에 인덱스로 접근해서 수정하거나 `length`를 변경하는 등
    * `Vue.set` 이나 `splice`를 활용하세요.
* non-mutating 하고 싶다면 - `filter()` `concat()` `slice()` 사용
  * 데이터 레퍼런스 변경됐다고 기존 DOM을 다 버리고 렌더링 하지는 않으니 걱정ㄴㄴ

### 객체
* vue instance 생성 시점에 선언이 안 되어 있었다면 바인딩도 안 되는 한계는 이렇게 해결할 수 있습니다.
* `Vue.set(obj, key, val)`으로 동적 추가 가능합니다.
  * == `vm.$set`
* 혹은 기존의 obj를 확장해서 아래처럼 재할당 하시면 되여.

```js
this.userProfile = Object.assign({}, this.userProfile, {
  age: 27,
  favoriteColor: 'Vue Green'
})
```

## `v-for`와 컴포넌트 같이 쓸 수 있는데요
이 때는 컴포넌트의 독립된 스코프를 보장하기 위해, 데이터를 자동으로 주입하지 않음. (명시적으로 넣어 주어야 함)
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
[MVC, MVP, MVVM](https://magi82.github.io/android-mvc-mvp-mvvm/)... 
구글링하다 '이런 패턴은 왜 쓰나'에 대한 한 문장 정리 맘에 들어서.

> 화면에 보여주는 로직과 실제 데이터 처리 로직을 분리
