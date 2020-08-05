---
layout: post
title: '[NodeJS] ES6 on Node.js using Babel'
author: HyeGyeong
categories: [NodeJS, Babel]
image: 'assets/images/babel.jpg'
sitemap:
  changefreq: daily
  priority: 1.0
---

## What is [Babel](https://babeljs.io/)?

- 최신의 Javascript(ES6 이상)를 예전(표준으로 볼 수 있는) Javascript 코드로 변환해줌. 구형 브라우저(IE같은...)에서는 최신 Javascript를 지원하지 않기 때문에 babel을 이용하여 대부분의 브라우저에서 호환되도록 바꿔야 함.
  ![walking](/blog/assets/images/babel_example.png 'What is babel?')

## Babel은 여러 Loader가 있는데 현재는 babel node 이용.

- `npm install @babel/node`로 다운

## babel preset(뜻: 미리 조정하다)?

- 각 문법 별로 독립적인 **플러그인(Plugin)**을 제공하는데 이 플러그인들을 한번에 적용할 수 있도록 모아놓은 것을 **프리셋(Preset)**이라 한다.
- env:
  - stage3 이상의 문법 플러그인들을 포함한다.
  - `npm install @babel/preset-env`
- stage0, stage1, stage2, stage3 등도 있다. (나중에 정리 예정.)

## .babelrc file?

- babel을 설정하기 위한 파일.

```json
// .babelrc
{
  "presets": ["@babel/preset-env"]
  // 사용하는 preset으로 변경해서 세팅해줌.
}
```

```json
// package.json

"scripts": {
// "start": "node index.js
  "start": "babel-node index.js"
}
/*
- index.js 파일을 node 대신 babel이 실행하도록 명령어 수정
- babel이 최신 javascript 문법을 낮은 버전의 문법으로 변환한 뒤, node로 실행함.
*/
```

- `npm start` 전에 `npm install @babel/core` 진행
