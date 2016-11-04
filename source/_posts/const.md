---
title: const
date: 2016-11-04 17:37:36
category:
- JavaScript
- ES6
---

내친김에 const도.

## const

1. 재 할당 안 됨.
2. immutable 아님.

```js
const numLivesForCat = 9;
const kitty = {
    name: "Aurora",
    numLives: numLivesForCat,
}

// Error
kitty = {
    name: "Danielle",
    numLives: numLivesForCat
};

// all OK
// 참고) 타입스크립트에선 안 됨.
kitty.name = "Rory";
kitty.name = "Kitty";
kitty.name = "Cat";
kitty.numLives--;
```

