---
layout: post
title: '[JS-Basic] ES6 Arrow Function'
author: HyeGyeong
categories: [js-basic]
image: 'assets/images/javascript.jpeg'
sitemap:
  changefreq: daily
  priority: 1.0
---

## 화살표 함수 (Arrow Function)

```js
// way 1
[1, 2, 3].map(function(n) {
  return Math.pow(n, 2);
}); // [1, 4, 9]

// way 2
[1, 2, 3].map(n => {
  return Math.pow(n, 2);
}); // [1, 4, 9]

// way 3
[1, 2, 3].map(n => {
  return n ** n;
}); // [1, 4, 9]

// way 4
[1, 2, 3].map(n => n ** n); // [1, 4, 9]
```

- 위의 함수는 모두 같은 값을 리턴한다.
- 화살표함수는 암묵적으로 `return`을 가지기 때문에 **way4**처럼 `실행문이 1개`일 때 `중괄호({})와 return을 생략`할 수 있다.

```js
const add = (x, y) => {
  console.log(x, y);
  return x + y;
};
```

- 위와 같이 `실행문이 2개 이상`일 때는 중괄호({})로 묶고 return값이 있다면 return을 적어줘야 한다.

## 화살표 함수의 this 바인드

- [일반 함수의 this](https://blog.hyegyeong.com/this/)
- 화살표 함수의 this는 자신만의 `this`를 생성하지 않는다.

```js
function exFunc() {
  var that = this;
  that.num = 0;
  setInterval(function add() {
    // setInterval의 this는 exFunc의 this가 아니기 때문에 다른 변수에 this를 지정해서 사용해야 한다.
    that.num++;
    console.log(that.num); // 1초마다 1씩 증가시킨 that.num을 찍어줌.
  }, 1000);
}
```

- 화살표 함수는 자신의 this가 바인드 되지 않아서 함수 스코프의 this가 적용된다. 즉, `상위 함수의 this`를 그대로 사용할 수 있다.

```js
function exFunc() {
  this.num = 0;
  setInterval(() => {
    this.num++; // 여기에서의 this는 exFunc의 this이다.
    console.log(this.num);
  }, 1000);
}
```

#### 표준은 ES6로 사용하되, `this`를 사용할 때는 경우에 따라 화살표함수(()=>{})와 일반 함수(function(){}) 중 선택하면 된다.
