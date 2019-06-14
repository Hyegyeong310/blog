---
layout: post
title: '[NodeJS] Helmet Middlewares'
author: HyeGyeong
categories: [NodeJS, Express]
image: 'assets/images/express.png'
sitemap:
  changefreq: daily
  priority: 1.0
---

## [Helmet](https://www.npmjs.com/package/helmet)

- node.js app 보안에 도움을 줌.
- HTTP 헤더를 적절히 설정하여 웹 취약성으로부터 앱을 보호할 수 있다.
- Helmet을 설치하면 아래의 더 작은 미들웨어들을 사용할 수 있다.

  - csp: Content-Security-Policy 헤더를 설정하여 XSS(Cross-site scripting) 공격 및 기타 교차 사이트 인젝션을 예방한다.
  - hidePoweredBy: X-Powered-By 헤더를 제거한다.
  - hpkp: Public Key Pinning 헤더를 추가하여, 위조된 인증서를 이용한 중간자 공격을 방지한다.
  - hsts: 서버에 대한 안전한(SSL/TLS를 통한 HTTP) 연결을 적용하는 Strict-Transport-Security 헤더를 설정한다.
  - ieNoOpen: IE8 이상에 대해 X-Download-Options를 설정한다.
  - noCache: Cache-Control 및 Pragma 헤더를 설정하여 클라이언트 측에서 캐싱을 사용하지 않도록 한다.
  - noSniff: X-Content-Type-Options를 설정하여, 선언된 콘텐츠 유형으로부터 벗어난 응답에 대한 브라우저의 MIME 가로채기를 방지한다.
  - frameguard는 X-Frame-Options 헤더를 설정하여 clickjacking에 대한 보호를 제공한다.
  - xssFilter: X-XSS-Protection을 설정하여 대부분의 최신 웹 브라우저에서 XSS(Cross-site scripting) 필터를 사용하도록 한다.

  > [express 프로덕션 우수 사례: 보안](https://expressjs.com/ko/advanced/best-practice-security.html)

- 설치
  `npm install helmet`

- 사용

```js
import express from 'express';
import helmet from 'helmet';

const app = express();

const handleIndex = (req, res) => res.send('Hello from Index');

app.use(helmet());

app.get('/', handleIndex);
```

### 몇 가지 잘 알려진 웹 취약성으로부터 앱을 보호할 수 있기 때문에 잘 모르더라도 사용하는 버릇을 들이면 좋다.
