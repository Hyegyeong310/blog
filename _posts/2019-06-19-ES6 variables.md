---
layout: post
title: '[JS-Basic] ES6 variables'
author: HyeGyeong
categories: [js-basic]
image: 'assets/images/javascript.jpeg'
sitemap:
  changefreq: daily
  priority: 1.0
---

## const, let

#### 블록 스코프 (block scope)

- 처음 javascript를 배울 때 `var`로 시작했고, jquery를 이용한 프로젝트를 진행할 때도 var를 사용하는데 익숙해서 let, const가 나왔다고는 해도 딱히 써 볼 생각을 안 했는데 React, Node.js를 사용하다보니 let, const의 장점이 와닿기 시작했다.(아직 멀었지만ㅋㅋㅋ)

```js
if (true) {
  var x = 5;
}
console.log(x); // 5

if (true) {
  const y = 3;
}
console.log(y); // ReferenceError: y is not defined
```

- `var`는 **함수 스코프**, `let, const`는 **블록 스코프**를 가진다.
- `let, const`는 블록`{}` 안에서만 접근할 수 있다.
- `var`는 if, for, while 등은 함수가 아니기 때문에 호이스팅의 문제가 발생했다. 작업하다보면 제일 빡침.

```js
// 전에 엄청 고생했던 문제가 있었는데 못 찾겠음. 대략 이런 느낌...?
var arr = [];
for (var i = 0; i < 3; i++) {
  arr[i] = function() {
    console.log(i);
  };
}
for (var j = 0; j < 3; j++) {
  arr[j]();
}
/*
원하는 결과: 0, 1, 2
실제 결과: 3, 3, 3

var는 함수 스코프이기 때문에 
arr[i] = function(){
  console.log(i); <= 이 부분에 for문이 다 돌고 난 다음의 i 값인 3이 들어감.
}
*/

// solution 1
var arr = [];
function val(num) {
  return function() {
    console.log(num);
  };
}
for (var i = 0; i < 3; i++) {
  arr[i] = val(i);
}
for (var j = 0; j < 3; j++) {
  arr[j](); // 0, 1, 2
}

// solution 2
const arr = [];
for (let i = 0; i < 3; i++) {
  arr[i] = () => console.log(i);
}
for (let j = 0; j < 3; j++) {
  arr[j](); // 0, 1, 2
}
```

#### const와 let의 차이

- const(constant)
  - 한 번 대입하면 다른 값을 대입할 수 없음. 상수.
  - 선언과 대입을 함께 해야 함.
  - But!!! Array([]), Object({})를 const로 선언하고 그 데이터 값을 변경할 수 있음
  ```js
  const a = 0;
  a = 1; // 에러 발생!
  const b = [];
  b.push(1);
  b.push(2);
  console.log(b); // [1, 2]
  ```
- let
  - `var`와 용도는 비슷. 선언하고 값을 변경할 수 있다.
  ```js
  let a = 0;
  a = 1;
  console.log(a); // 1
  ```

#### 기본적으로 const를 사용하고 다른 값을 대입할 필요가 있을 때 let을 사용한다.
