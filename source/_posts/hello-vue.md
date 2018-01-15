---
title: Vue.js
date: 2018-01-15 16:37:00
category:
- JavaScript
- Vue.js
---

JS 프레임워크 ~~백년~~전쟁에 결론이 날 때가 되었다더라.

### 짧게, 왜 Vue ?
https://www.sitepen.com/blog/2017/11/10/web-frameworks-conclusions/ 발췌
* 일단 프레임 워크의 비용 합리적이라 판단해야겠지만...

\ | good | bad | future | Why would I choose...
---|---|---|---|---
앙2+| 구글으인기 + 교재의양 | 유지보수 누가해... | 웹표준과 쫌 다른 노선(web component, pwa등) | 이미 잘 쓰고 있었다면 할만 함. 아니면 만드려는게 모델-뷰 패턴에 꼭 맞으면 갠춘. 혹은 Material UI 편하게 쓰구 싶다면.
React<br>Redux| 단순 | 추가 기능 솔루션 파편화 | 반반 | 러닝커브 완만
Vue.js| 간결한 구조, 열정적인 개발자 커뮤니티, 검증된 추가 솔루션들 | 이거슨 모델-뷰 응용인가 상태 컨테이너인가 그런 헷갈림이 있다고 함. 개발자 한 명이 책임지는 불안함 | 아직 나쁜 징후 없음 | 베스트 프랙티스 교재가 존재함. 프레임웍 적용의 범위를 개발자가 결정 할 수 있음

### 솔깃해져서 vue의 getting started를 읽어봄.
> 다른 단일형 프레임워크와 달리 Vue는 점진적으로 채택할 수 있도록 설계하였습니다.

기존 플젝 소스를 다 버려야 하는 앙귤러를 써본 터라 '점진적 적용'이 가장 솔깃함. 뷰의 코어는 말 그대로 뷰 레이어에만 관여하는 듯 -> 다른 라이브러리 생각 않고 레거시에 붙이기 가능하다니 멋져...! 그리고도 [매력발산](https://kr.vuejs.org/v2/guide/comparison.html) 많이 할 수 있는듯. [공식 라이브러리도 많고](https://github.com/vuejs/awesome-vue#components--libraries) 그리고 이 모든것보다 우선하여, **문서가 잘 되어 있다**는 점 가장 채고.

### Vue basic
#### 선언 렌더링 - 데이터와 DOM은 REACTIVE
```html
<div id="app">
  {{ message }}
</div>
```
```js
var app = new Vue({
  el: '#app',
  data: {
    message: 'Hi Vue!' // app.message로 접근 & 변경가능 -> DOM update
  }
})
```
#### `v-` DIRECTIVE (지시)
렌더링된 돔에 특수한 반응형 동작을 지시함
```html
<div id="app-2">
  <span v-bind:title="message">
    span title 필드에 app2.message를 'keep' 바인딩
  </span>
</div>
```
```js
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: 'Hi Again!'
  }
})
```
* `v-bind:(prop)`
* `v-if=(조건구문)`, `v-for="(반복구문)"` - 텍스트, 속성 뿐 아니라 DOM 구조에도 데이터 바인딩 가능
* `v-on:(eventName)` - 이벤트 리스너 선언 가능
* `v-model="(prop)"` - 양방향 바인딩 가능

#### (웹) 컴포넌트 like 시스템
```html
<div id="app-7">
  <ol>
    <todo-item
      v-for="item in groceryList"
      v-bind:todo="item"
      v-bind:key="item.id">
    </todo-item>
  </ol>
</div>
```
```js
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})

var app7 = new Vue({
  el: '#app-7',
  data: {
    groceryList: [
      { id: 0, text: 'Vegetables' },
      { id: 1, text: 'Cheese' },
      { id: 2, text: 'Whatever else humans are supposed to eat' }
    ]
  }
})
```

### (부록) vue는 MVVM
#### 잠깐, MVC MVP MVVM... 패턴은 왜 쓰냐
화면에 보여주는 로직과 실제 데이터 처리 로직을 분리

#### view model
![mvvm](https://magi82.github.io/images/2017-2-24-android-mvc-mvp-mvvm/mvvm.png)

#### See More
[MVC, MVP, MVVM 비교](https://magi82.github.io/android-mvc-mvp-mvvm/)
