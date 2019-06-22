---
layout: post
title: '[NodeJS] path module (__filename, __dirname)'
author: HyeGyeong
categories: [Express, NodeJS]
image: 'assets/images/express.png'
sitemap:
  changefreq: daily
  priority: 1.0
---

## path module

- 경로 처리를 도와주는 express 모듈.

#### \_\_filename

- 현재 파일명에 대한 정보를 담고 있는 변수

#### \_\_dirname

- 현재 파일 경로에 대한 정보를 담고 있는 변수

```js
// filename.js
console.log(__filename);
console.log(__dirname);
```

![path Module example](https://user-images.githubusercontent.com/25483027/59965611-76d0ec00-954b-11e9-9dfe-21a182654de7.png)

- 각자의 컴퓨터마다 다르게 나옴. `build`할 때 달라진 경로를 `path module`로 처리할 수 있다.
