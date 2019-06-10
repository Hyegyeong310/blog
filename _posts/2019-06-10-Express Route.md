---
layout: post
title: '[NodeJS] Express Route'
author: HyeGyeong
categories: [NodeJS, Express]
image: 'assets/images/express.png'
sitemap:
  changefreq: daily
  priority: 1.0
---

## Route

- GET: 요청받은 URL의 정보를 검색하여 응답(response)한다.
- POST: 데이터 전송. 클라이언트에서 서버로 어떤 정보를 제출한다.
- PUT: 보통 데이터 갱신할 때 사용.
- DELETE: 데이터 삭제.

## GET

- 웹사이트에 들어가게 되면, 예를 들어 `https://www.google.com/`에 들어가는 경우, 브라우저가 그 URL로 GET method를 실행한다.
- 브라우저가 response에 담긴 정보(html, css, js 등)를 읽는다.
- GET method는 정보를 보낼 수 없다.

## POST

- 브라우저가 웹사이트에 어떤 정보를 전달할 때 사용하는 method.
- 예를 들어 웹사이트에서 로그인을 할 때, 브라우저가 웹사이트에 POST method를 통해 로그인 정보를 전달한다. 로그인 정보에 해당하는 response를 브라우저로 보낸다.
- Login, Join, Comment 등...

```js
// index.js
const express = require('express');
const app = express();

const PORT = 4000;

app.get('/', (req, res) => {
  /*
  - req(request), res(response)는 express 메소드에서 제공하는 Objects arguments.
  - req에는 누가 페이지를 요청했는가, 어떤 종류의 데이터가 페이지로 전송됐는가 등의 정보가 담긴다.
  - 만약 response가 없으면 무한 로딩.
  */
  res.send('Hello World!!');
});

app.get('/other', (req, res) => {
  // get method의 첫번째 인자는 '라우트 경로'
  // `http://localhost:${PORT}/other` 에서 결과 확인 가능
  res.send('This is other page!');
});

app.listen(PORT, (req, res) => {
  console.log(`Listening on: http://localhost:${PORT}`);
});
```
