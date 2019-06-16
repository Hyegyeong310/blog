---
layout: post
title: '[NodeJS] Other Middlewares'
author: HyeGyeong
categories: [NodeJS, Express]
image: 'assets/images/express.png'
sitemap:
  changefreq: daily
  priority: 1.0
---

## [cookie parser](https://www.npmjs.com/package/cookie-parser) Middleware

- express middleware
- cookie를 다룰 수 있도록 도와줌.
- `npm install cookie-parser`로 설치
- cookie에 필요한 정보를 저장할 수 있게 해준다.

## [body parser](https://www.npmjs.com/package/body-parser) Middleware

- express middleware
- body를 다룰 수 있도록 도와줌.
- `npm install body-parser`로 설치
- form의 정보를 채워서 전송하면 그 데이터는 request object 형태로 서버에 의해 받아진다.

```js
import express from 'express';
import cookieParser from 'cookie-parser';
import bodyParser from 'body-parser';

const app = express();

app.use(cookieParser());
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));
/*
bodyParser는 옵션이 있음. json, text, urlencoded
어떤 형식의 데이터를 전송하는지 서버에 알려주는 기능.
*/

app.post('/profile', (req, res) => {
  console.log(req.body);
  // `body-parser`를 이용하지 않으면 아래의 `req.body`는 `undefined`로 나온다.
});
```

- express v4.x 기준으로 express에 body parser가 빌트인 되었음.
  > 출처: [Express Docs](https://expressjs.com/en/4x/api.html#express-json-middleware)

```js
import express from 'express';

const app = express();

app.use(express.json());
app.use(express.urlencoded({ extended: true }));

app.port('/profile', (req, res) => {
  console.log(req.body);
});
```

와 같이 사용할 수 있다.
