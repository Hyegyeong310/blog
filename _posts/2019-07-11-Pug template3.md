---
layout: post
title: '[NodeJS] Pug Template3'
author: HyeGyeong
categories: [Express, NodeJS]
image: 'assets/images/pug.png'
sitemap:
  changefreq: daily
  priority: 1.0
---

## Pug Template 3

#### pug 안에 Javascript 추가하기

1. javascript 외의 text가 없을 때

- `tag=javascript code`를 작성한다.

```pug
// footer.pug
footer
  span=(new Date().getFullYear())

// html
<footer>
  <span>2019</span> // 현재 년도
</footer>
```

2. javascript 외의 text가 있을 때

- `#{}` 안에 코드를 작성한다.

```pug
// footer.pug
footer
  span © #{new Date().getFullYear()}

// html
<footer>
  <span>© 2019</span>
</footer>
```

#### pug 템플릿에 변수, 정보를 전달하기

1. 템플릿 전체에 전달 (middleware를 이용하여 local 변수 설정)

- [Middleware 포스팅 바로가기](https://hyegyeong310.github.io/blog/Express-Middleware/)

```js
// app.js

import express from 'express';
const app = express();

const localsMiddleware = (req, res, next) => {
  res.locals.siteName = 'Goob pug!';
  next();
};
app.use(localsMiddleware);
```

```pug
// main.pug
doctype html
html
  head
    title #{siteName}
  body
    include ../partials/header
    main
      block content
    include ../partials/footer

// html
<html>
  <head>
    <title>Goob pug!</title>
  </head>
  <body>
    <header>...</header>
    <main>
      ...
    </main>
    <footer>...</footer>
  </body>
</html>
```

> [express locals 문서](https://expressjs.com/ko/api.html#res.locals)

2. 각각 템플릿에 전달

```js
// app.js

app.get('/', (req, res) => {
  // render 메소드의 1번째 인자는 템플릿,
  // 2번째 인자는 템플릿에 추가할 정보가 담긴 객체
  res.render('home', { pageName: 'Home' });
});

app.get('/login', (req, res) => {
  res.render('login', { pageName: 'Login' });
});
```

- render함수에서 보내주는 `pageName` 변수를 사용함.

```pug

// home.pug
doctype html
html
  head
    title #{pageName} | #{siteName}

// login.pug
doctype html
html
  head
    title #{pageName} | #{siteName}

// home html
<html>
  <head>
    <title>Home | Goob pug!</title>
  </head>
</html>

// login html
<html>
  <head>
    <title>Login | Goob pug!</title>
  </head>
</html>
```
