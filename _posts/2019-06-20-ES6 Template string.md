---
layout: post
title: '[JS-Basic] ES6 Template string'
author: HyeGyeong
categories: [js-basic]
image: 'assets/images/javascript.jpeg'
sitemap:
  changefreq: daily
  priority: 1.0
---

## 템플릿 문자열

- `'', ""`외에 ``로 감싸는 문자열 방식이 생겼다.

```js
// es5
var num1 = 1;
var num2 = 2;
var string = num1 + ' 더하기 ' + num2 + '는 ' + (num1 + num2);
console.log(string); // 1 더하기 2는 3

var string2 = '"안녕하세요." 철수가 말했다.';
console.log(string2); // "안녕하세요." 철수가 말했다.

var string3 = "I'm a girl.";
console.log(string3); // I'm a girl.
```

- ES5까지는 위와 같이 `+` 또는 `,`로 구분해야 했는데 쓰다보면 헷갈리고 어느 부분을 띄어야 되는지 생각해야되는 문제가 있었다.

```js
// es5
var string4 = '"I\'m a boy." 철수가 말했다.';
console.log(string4); // "I'm a boy." 철수가 말했다.
```

- ', "만 사용할 때는 표현하고자하는 문자열에 '가 있으면 ""으로 감싸고, "가 있으면 ''로 감싸야해서 왔다갔다 해야되는 것도 문제였지만 위와 같이 ''로 감싼 문자열 안에서 ''를 써야하는 경우도 왕왕 있다. 그럴 땐 역슬래쉬(\\)를 이용해서 무시되도록 해야한다.

```js
// es6
const num1 = 1;
const num2 = 2;
const string = `${num1} 더하기 ${num2}는 ${num1 + num2}`;
console.log(string); // 1 더하기 2는 3;

const string2 = `"안녕하세요." 철수가 말했다.`;
console.log(string2); // "안녕하세요." 철수가 말했다.

const string3 = `I'm a girl.`;
console.log(string3); // I'm a girl.

const string4 = `"I'm a boy." 철수가 말했다.`;
console.log(string4);
```

- ES6의 템플릿 문자열을 쓰면 위와 같이 가독성도 좋고 그저 문법만 맞춰 써주면 된다. 변수 위치를 `${}`로 묶어주면 끝!
- ``(백틱)이 생김으로써 편하게 글 쓰듯 사용할 수 있게 되었다.
- `는 백틱이라 부르고 mac 기준으로 caps lock + ~ 를 누르면 된다. (내 맥북에는 백틱이 표시되어 있지 않아 몰라서 못 썼던 기억이...ㅜㅜ)
