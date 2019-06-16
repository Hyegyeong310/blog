---
layout: post
title: '[NodeJS] Express Middleware'
author: HyeGyeong
categories: [NodeJS, Express]
image: 'assets/images/express.png'
sitemap:
  changefreq: daily
  priority: 1.0
---

## Express Middleware

- 말 그대로 가운데(middle)에 있는 소프트웨어를 의미함.
- 마지막 처리가 될 때까지 연결해서 다음 함수를 실행할 수 있도록 한다.
- 처리가 끝날 때까지 연결되어 있음. (linked list 같은 느낌?)
- 유저와 마지막 응답 사이에서 작동하는 것을 Middleware라 함.
- Express의 모든 함수는 Middleware가 될 수 있다.

```js
// index.js
import express from 'express';

const app = express();

const handleIndex = (req, res) => res.send('Hello, This is Index');
const betweenIndex = (req, res, next) => {
  console.log('This is betweenIndex');
  next();
};

app.get('/', betweenIndex, handleIndex);
// user가 '/'를 요청했을 때 betweenIndex를 거쳐 handleIndex를 실행한다.
// betweenIndex가 여기서 Middleware인데 next를 실행하지 않으면 handleIndex로 넘어갈 수 없다.
```

- Express의 모든 route와 함수 등 connection을 다루는 것은 request, response, next를 가지고 있다.
- 마지막 함수의 경우 next를 이용할 필요가 없어서 (req, res)만 다룬다. 다만 유저에게 무언가를 return한다.
- 위의 예시에서는 '/' route를 요청했을 때만 betweenIndex Middleware를 사용한다. 모든 요청에서 사용하고 싶다면

```js
app.use(betweenIndex);
// 이 부분에 필요한 만큼 Middleware를 추가할 수 있다.
// 다만 필요한 기능을 순서에 맞게 추가해야 한다.

app.get('/', handleIndex);
```

와 같이 할 수 있다. Javascript는 위에서 아래로 진행하는 스크립트 언어기 때문에 **순서 중요!!!**

- Middleware에서 res.send를 실행하면 연결을 끊을 수 있다.

```js
const handleIndex = (req, res) => res.send('Hello, This is Index');
const betweenIndex = (req, res, next) => {
  res.send('This is betweenIndex');
};

app.get('/', betweenIndex, handleIndex);
```

- 위와 같이 route 전에 res.send를 실행하는 middleware를 넣으면 연결이 끊겨서 `handleIndex` 함수를 실행할 수 없다. next를 실행하지 않으면 최종 실행 함수와 같아진다. **res.send를 middleware에 사용할 땐 주의할 것!**
