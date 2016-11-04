---
title: Hello! TypeScript
date: 2016-11-04 18:44:05
category:
- JavaScript
- TypeScript
---

네가 나에게 타입을 선언해주었을 때 나는 타입 언어가 되었다. 

### Quick

런타임시에는 checking 코드가 없음. 컴파일 시에 validate.  
컴파일 시에 invalid 하다고 해서 코드를 없애거나 수정하지는 않음. 

#### 1
```ts
type C = {a: string, b?: number}

function f({a, b}: C = {a: "", b: 0}): void {
    //...
}
f({a:'1',b: 1}); // ok
f(); // ok, default to {a: "", b: 0}
f({a:'1',b: '1'}); // Error
f({a: 'asdf'}); // ok
f({b: 1}); // Error
```
```js
//compiled
function f(_a) {
    var _b = _a === void 0 ? { a: "", b: 0 } : _a, a = _b.a, b = _b.b;
    //...
}
f({ a: '1', b: 1 }); // ok
f(); // ok, default to {a: "", b: 0}
f({ a: '1', b: '1' }); // Error
f({ a: 'asdf' }); // ok
f({ b: 1 }); // Error
```

#### 2

```ts
interface Person {
    firstName: string;
    lastName: string;
}

class Student {
    fullName: string;
    constructor(public firstName, public middleInitial, public lastName) {
        this.fullName = firstName + ' ' + middleInitial + ' ' + lastName;
    }
}

function greeter(man: Person) {
    return 'Hello, ' + man.firstName + ', ' + man.lastName;
}

// var user = {firstName: 'juhee', lastName: 'bak'};
var user = new Student('Juhee', 'June', 'Bak');
```
```js
//compiled
var Student = (function () {
    function Student(firstName, middleInitial, lastName) {
        this.firstName = firstName;
        this.middleInitial = middleInitial;
        this.lastName = lastName;
        this.fullName = firstName + ' ' + middleInitial + ' ' + lastName;
    }
    return Student;
}());

function greeter(man) {
    return 'Hello, ' + man.firstName + ', ' + man.lastName;
}

// var user = {firstName: 'juhee', lastName: 'bak'};
var user = new Student('Juhee', 'June', 'Bak');
```

### Basic Types
#### Boolean
```ts
let flag :boolean = false;
```
```js
//compiled
var flag = false;
```

`--strictNullChecks` 옵션을 사용하지 않는 경우, 모든 타입에 `null`, `undefined` 할당 가능.
#### Number
```ts
let decimal: number = 6;
```
```js
//compiled
var decimal = 6;
```
#### String
```ts
let str:string = 'a';
let concat:string = "test" + " " ;
let join:string = ["test", " "].join() ;
let template:string = `Hello, my name is ${ str + 'embedded expressions' }.`;
```
```js
//compiled
var str = 'a';
var concat = "test" + " ";
var join = ["test", " "].join();
var template = "Hello, my name is " + (str + 'embedded expressions') + ".";
```
#### Array
```ts
let nlist:number[] = [1,2,3];
let alist:Array<number> = [1,2,3];
```
```js
//compiled
var nlist = [1, 2, 3];
var alist = [1, 2, 3];
```
#### Tuple
```ts
let tuple:[string, number] = ['hello', 1];
tuple[3] = "world"; // OK, 'string' can be assigned to 'string | number'
console.log(tuple[5].toString()); // OK, 'string' and 'number' both have 'toString'
tuple[6] = true; // Error, 'boolean' isn't 'string | number'
```
```js
//compiled
var tuple = ['hello', 1];
tuple[3] = "world";
console.log(tuple[5].toString());
tuple[6] = true;
```
#### Enum
```ts
enum Color {Red, Green, Blue};
let c:Color = Color.Green;
enum Color_ {Red = 1, Green, Blue};
let colorName:string = Color[2];
```
```js
//compiled
var Color;
(function (Color) {
    Color[Color["Red"] = 0] = "Red";
    Color[Color["Green"] = 1] = "Green";
    Color[Color["Blue"] = 2] = "Blue";
})(Color || (Color = {}));
;
var c = Color.Green;
var Color_;
(function (Color_) {
    Color_[Color_["Red"] = 1] = "Red";
    Color_[Color_["Green"] = 2] = "Green";
    Color_[Color_["Blue"] = 3] = "Blue";
})(Color_ || (Color_ = {}));
;
var colorName = Color[2];
```
#### Any
```ts
let notSure: any = 4;
notSure = "maybe a string instead";
notSure = false; // okay, definitely a boolean
let anyList: any[] = [1, true, "free"];
anyList[1] = 100;
```
```js
//compiled
var notSure = 4;
notSure = "maybe a string instead";
notSure = false; // okay, definitely a boolean
var anyList = [1, true, "free"];
anyList[1] = 100;
```
#### Void
```ts
function voidFunc():void{
    console.log('a');
}
let unusable: void = undefined;
unusable = null;
```
```js
//compiled
function voidFunc() {
    console.log('a');
}
var unusable = undefined;
unusable = null;
```
#### Null & Undefined
귀찮아서 잘 안 하지만 `--strictNullChecks` 플래그 사용하면 `null`과 `undefined`는 `void` 타입에만 할당가능.  
이 옵션을 쓰면서 특정 타입에 `null` 이나 `undefined`를 쓰려면 `string | null | undefined` 처럼 union type으로 선언할 것.

#### Never
```ts
function error(message: string): never {
    throw new Error(message);
}
```
```js
//compiled
function error(message) {
    throw new Error(message);
}
```
#### Type assertion
"날 믿어 컴파일러야. 나 지금 뭐 하는지 알아."  

```ts
let someValue: any = "this is a string";
let strLength: number = (<string>someValue).length;
let strLength2: number = (someValue as string).length;
```
```js
//compiled
var someValue = "this is a string";
var strLength = someValue.length;
var strLength2 = someValue.length;
```