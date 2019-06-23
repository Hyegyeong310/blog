---
layout: post
title: '[NodeJS] Pug Template1'
author: HyeGyeong
categories: [Express, NodeJS]
image: 'assets/images/pug.png'
sitemap:
  changefreq: daily
  priority: 1.0
---

## Pug Template 1

- Express view engine
- `npm install pug`로 설치 할 수 있다.
- express의 view engine의 기본값은 `undefined`인데, set()을 통해서 view engine을 `pug`로 변경할 수 있다.

```js
import express from 'express';
const app = express();

app.set('view engine', 'pug');
```

- pug와 express에는 view 파일들 위치에 대한 기본 설정이 있다. 기본값은 `views` 폴더이고, 변경하고 싶다면 express.set('views', '새로운 파일경로')를 이용한다.
  > [express 공식문서](https://expressjs.com/ko/api.html#app.set)

![image](https://user-images.githubusercontent.com/25483027/59974163-bc40f800-95e3-11e9-9b5b-5c245243e2a9.png)

- pug는 들여쓰기가 중요한 언어.
  - 일반 html과 같은 태그를 사용하지 않고 태그 이름을 적으면 된다.
  - 들여쓰기로 태그 안에 있는 요소를 만들 수 있다.

```pug
// home.pug
.container // class가 'container'인 div
  p Hello! // .container 안의 p 태그
```

```html
<div class="container">
  <p>Hello!</p>
</div>
```

- 템플릿을 웹사이트에 보여주기 위해서는 `res.send()` 대신 `res.render()`를 사용한다.

```js
app.get('/', (req, res) => res.render('home'));
```

- 위와 같이 render( ) 안에 인자로 템플릿 파일의 이름을 입력한다. 그러면 `render함수`가 `views 폴더`에서 `파일명이 home`이고 `확장자가 pug`인 템플릿 파일을 찾은 후 보여준다.
