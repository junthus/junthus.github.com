---
title: destructuring
date: 2016-11-04 17:48:06
category:
- JavaScript
- ES6
---

구조를 파★개☆한★다☆

## Array

```js
let input = [1, 2];
let [first, second] = input;
console.log(first); // 1
console.log(second); // 2
```

better than

```js
first = input[0];
second = input[1];
```

#### default values
```js
let [first=1, second=2] = [3];

console.log(first); // 3
console.log(second); // 2
```

#### swap
```js
[first, second] = [second, first];
```

#### parameters
```js
let input = [1, 2];
function f([first, second]) {
    console.log(first);
    console.log(second);
}
f(input);
```

```js
let [first, ...rest] = [1, 2, 3, 4];
console.log(first); // 1
console.log(rest); // [ 2, 3, 4 ]
```

### 오 mdn 꿀팁 - url 분해
```js
var url = "https://developer.mozilla.org/en-US/Web/JavaScript";

var parsedURL = /^(\w+)\:\/\/([^\/]+)\/(.*)$/.exec(url);
console.log(parsedURL); // ["https://developer.mozilla.org/en-US/Web/JavaScript", "https", "developer.mozilla.org", "en-US/Web/JavaScript"]

var [, protocol, fullhost, fullpath] = parsedURL;

console.log(protocol); // "https"
```

## Object

```js
let o = {
    a: "foo",
    b: 12,
    c: "bar"
}
let {a, b} = o;
```

선언부와 분리해서 할당하... 하... 왜때문에 이런 모양...

```js
let a,b;

//...

({a, b} = {a: "baz", b: 101});
```

#### Property renaming

```js
var o = {p: 42, q: true};
var {p: foo, q: bar} = o;
 
console.log(foo); // 42 
console.log(bar); // true  
```

#### default values
```js
var {a=10, b=5} = {a: 3};

console.log(a); // 3
console.log(b); // 5
```

#### parameters
```js
function f({a, b = 0} = {a: ""}) {
    console.log(a);
    console.log(b);
} 

f(); // '', 0
f({a: t}); // 't', 0
```

### 와앙 또 mdn 꿀팁
[안되겠다 링크를 남겨야지](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

#### nested object 필드 추출
```js
var metadata = {
    title: "Scratchpad",
    translations: [
       {
        locale: "de",
        localization_tags: [ ],
        last_edit: "2014-04-14T08:43:37",
        url: "/de/docs/Tools/Scratchpad",
        title: "JavaScript-Umgebung"
       }
    ],
    url: "/en-US/docs/Tools/Scratchpad"
};

var { title: englishTitle, translations: [{ title: localeTitle }] } = metadata;

console.log(englishTitle); // "Scratchpad"
console.log(localeTitle);  // "JavaScript-Umgebung"
```
#### for of iteration 에서 필드 추출 
```js
var people = [
  {
    name: "Mike Smith",
    family: {
      mother: "Jane Smith",
      father: "Harry Smith",
      sister: "Samantha Smith"
    },
    age: 35
  },
  {
    name: "Tom Jones",
    family: {
      mother: "Norah Jones",
      father: "Richard Jones",
      brother: "Howard Jones"
    },
    age: 25
  }
];

for (var {name: n, family: { father: f } } of people) {
  console.log("Name: " + n + ", Father: " + f);
}

// "Name: Mike Smith, Father: Harry Smith"
// "Name: Tom Jones, Father: Richard Jones"
```

#### function parameter obj에서 필드 추출 
```js
function userId({id}) {
  return id;
}

function whois({displayName: displayName, fullName: {firstName: name}}){
  console.log(displayName + " is " + name);
}

var user = { 
  id: 42, 
  displayName: "jdoe",
  fullName: { 
      firstName: "John",
      lastName: "Doe"
  }
};

console.log("userId: " + userId(user)); // "userId: 42"
whois(user); // "jdoe is John"
```