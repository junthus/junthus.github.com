---
title: let
date: 2016-11-04 15:41:18
tags:
category:
- JavaScript
- ES6
---

let it go ~  
[타입스크립트 handbook](http://www.typescriptlang.org/docs/handbook/variable-declarations.html)에 `var` -> `let` 비교가 잘 되어 있어서 베낀다. 

## block scoping

function scope + 호이스팅 개객끼 문제가 있었음.

```js
function f(args) {
    a++; // OK(hoist)
    
    function capture(){
        return a; //OK
    }
    
    capture(); // returns 'undefined'
    
    var a = 10;
    
    if (args) {
        var b = a + 1;
    }

    return b;
}

f(true);  // returns '11'
f(false); // returns 'undefined'
```
없앴음.

```js
function f(args) {
    a++; // Error. 선언 전에 조작 노노
    
    function capture(){
        return a; //OK.
    }
    
    capture(); // Error
    
    let a = 10;
    
    capture(); // Returns 10
    
    if (args) {
        let b = a + 1;
        return b;     
    }
    
    return b;
}

f(true); // returns '11'
f(false); // Error
```

## Re-declarations and Shadowing

모든 `var`는 하나로 덮어졌었음.

```js
function f(x) {
    var x;
    var x;

    if (true) {
        var x;
    }
}
```

`let`: 안돼 안바꿔줘 돌아가.
```js
let x = 10;
let x = 20; // error: can't re-declare 'x' in the same scope
```
```js
function f(x) {
    let x = 100; // error: interferes with parameter declaration
}

function g() {
    let x = 100;
    var x = 100; // error: can't have both declarations of 'x'
}
```

let이 loop 변수로 쓰일 때는 조금 다르게 동작한다.   
iteration 마다 마치 새로운 스코프를 생성하는 것처럼 독립성을 보장한다(고 한다).   
그래서 for loop는 이제 i로만 써도 된다.  

```js
function sumMatrix(matrix/*: number[][]*/) {
    let sum = 0;
    for (let i = 0; i < matrix.length; i++) {
        var currentRow = matrix[i];
        for (let i = 0; i < currentRow.length; i++) {
            sum += currentRow[i];
        }
    }

    return sum;
}
```
## Block-scoped variable capturing
변수를 캡쳐하고 싶었는데.
```js
for (var i = 0; i < 2; i++) {
    setTimeout(function() { console.log(i); }, 100 * i);
}
// 2 
// 2 
// setTimeout에 전달하는 function은 모두 동일한 스코프의 i 를 바라봄.
```
그래서 이렇게 묶었어야 했는데.
```js
for (var i = 0; i < 10; i++) {
    (function(i) {
        setTimeout(function() { console.log(i); }, 100 * i);
    })(i);
}
// 0
// 1
```
루프 변수엔 `let`. 아윌 캡쳐 잇 포유. 저스트 레리꼬.
```js
for (let i = 0; i < 10 ; i++) {
    setTimeout(function() { console.log(i); }, 100 * i);
}
// 0
// 1

```