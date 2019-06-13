---
layout: post
title: '[NodeJS] Morgan Middleware'
author: HyeGyeong
categories: [NodeJS, Express]
image: 'assets/images/express.png'
sitemap:
  changefreq: daily
  priority: 1.0
---

## Morgan Middleware

- logging에 도움주는 npm package. (console.log와 비슷한 역할. 어디에서 무슨 일이 일어났는지 기록해 줌.)
- `npm install morgan` 으로 다운 가능.

```js
import express from 'express';
import morgan from 'morgan';

const app = express();

const handleIndex = (req, res) => res.send('Hello from Index');
const betweenIndex = (req, res, next) => {
  console.log('This is betweenIndex');
  next();
};

app.use(betweenIndex);
app.use(morgan('common'));

app.get('/', handleIndex);

// '/'로 요청이 오면 betweenIndex -> morgan -> handleIndex 순으로 실행
```

- [morgan](https://www.npmjs.com/package/morgan)은 logging 형식에 대한 옵션을 가지는데 `combined, common, dev, short, tiny`가 있다. `morgan(${option})`과 같이 원하는 형식으로 설정할 수 있다.

  - combined
    ![image](https://user-images.githubusercontent.com/25483027/59443283-a6d70b80-8e36-11e9-8d7a-82d56d016bd2.png)

  - common
    ![image](https://user-images.githubusercontent.com/25483027/59443336-c66e3400-8e36-11e9-842a-348a009a5a33.png)

  - dev
    ![image](https://user-images.githubusercontent.com/25483027/59443190-7db67b00-8e36-11e9-9c39-1d86b5b80e92.png)

  - short
    ![image](https://user-images.githubusercontent.com/25483027/59443398-df76e500-8e36-11e9-8efc-a44aca7b33c5.png)

  - tiny
    ![image](https://user-images.githubusercontent.com/25483027/59443446-f3bae200-8e36-11e9-94e3-bb0c234686b0.png)

- 어떤 접속(GET, POST 등)인지, 어디에 접속하는지(route), Status code 등을 알 수 있다.
