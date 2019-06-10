---
layout: post
title: '[NodeJS] My First Express Server'
author: HyeGyeong
categories: [NodeJS, Express]
image: 'assets/images/express.png'
sitemap:
  changefreq: daily
  priority: 1.0
---

## [Express](https://expressjs.com/) Getting Started

```js
// index.js

const express = require('express');
/*
require를 이용해서 express node module을 가져옴.
express 역시 많은 modules로 이루어져 있음. 작은 블럭들로 이루어져있다고 생각하면 됌.
node_modules -> express -> lib -> express.js 에서 내용 확인 가능.
*/
const app = express();
/*
  const로 선언한 변수 app에 express를 실행해서 담는다.
*/

const PORT = 4000;

app.listen(PORT, (req, res) =>
  console.log(`Listening on: http:localhost:${PORT}`)
);
```

terminal에서 `node [file name]`로 실행 가능.
예시 코드를 실행할 땐 `node index.js`
localhost:PORT에서 확인 가능. \${PORT}는 원하는 포트 넘버를 넣어준다.

## node [file name] 외의 방법

```json
// package.json

{
  "name": "example",
  "version": "1.0.0",
  "description": "This is an example",
  "author": "Hyegyeong310",
  "dependencies": {
    "express": "^4.17.1"
  },
  "scripts": {
    "start": "node index.js"
  }
}
```

package.json에 **scripts**를 추가한다. 일종의 명령어를 추가. 더 우아한 방법이다.
`npm start`로 server를 킬 수 있음.
server를 끌 때는 Mac 기준으로 `ctrl+c`
