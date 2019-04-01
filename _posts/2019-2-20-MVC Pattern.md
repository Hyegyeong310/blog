---
layout: post
title: 'MVC pattern'
author: HyeGyeong
categories: [2weeks-project, MVC]
image: 'assets/images/mvc-rails.png'
---

## MVC Pattern (Model, View, Controller)

- 현재 진행하는 프로젝트의 서버는 제대로 파일을 분리하지 않고 동작하면 그냥 넘기고 있었다. 한 파일에 모든 내용이 있는 상태라 필요한 부분, 오류가 난 부분 등 찾기가 쉽지 않았다. 2주 프로젝트가 끝날 때쯤 되서야 정리를 하다보니 마음은 급해졌지만 내가 짠 부분과 다른 팀원이 짠 부분을 모두 살펴봐야했기 때문에 서로 연결이 되고, 필요없는 부분을 제거하는 등 속시원한 것도 있다.

### MVC란?

> 모델-뷰-컨트롤러(Model–View–Controller, MVC)는 소프트웨어 공학에서 사용되는 아키텍처 패턴이다. 이 패턴을 성공적으로 사용하면, 사용자 인터페이스로부터 비즈니스 로직을 분리하여 애플리케이션의 시각적 요소나 그 이면에서 실행되는 비즈니스 로직을 서로 영향 없이 쉽게 고칠 수 있는 애플리케이션을 만들 수 있다. MVC에서 모델은 애플리케이션의 정보(데이터)를 나타내며, 뷰는 텍스트, 체크박스 항목 등과 같은 사용자 인터페이스 요소를 나타내고, 컨트롤러는 데이터와 비즈니스 로직 사이의 상호동작을 관리한다.
> (출처: 위키백과)

### M (Model)

- 데이터베이스 관련. 나는 Sequelize를 이용하여 데이터베이스를 검색하고 데이터를 받아오는 역할로 사용.

### V (View)

- 이 부분은 좀 더 확실히 알게 되면 정리. 현재는 서버쪽의 View는 app.js(index.js)를 의미하는 것 같음. Router를 call하는 쪽.

```js
// app.js
app.use('/', routes);

// route.js
const router = express.Router();
const controller = require('./controller');
router.get('/api', controller.api.get);
```

### C (Controller)

- Router와 Model을 연결해 주는 역할

```js
// controller.js
module.exports = {
  api: {
    get: (req, res) => {
      res.send("Hello!! Server on.");
    }
  }
```

### Controller와 Model 구성에 대한 고민

- User, Login, Match, Like 등 여러 api에 대한 구분을

```js
module.exports = {
  User: {
    getAllUsers: {...},
    getOneUsers: {...}
  },
  Login: {
    login: {...},
    logout: {...},
    signUp: {...}
  }
}
```

과 같이 정리했는데 좀 더 쪼개서 필요한 부분에 따라 폴더를 나눠서 그 안에서 모듈화하는 것이 더 직관적이었을 것 같다. 4주 프로젝트 이후에 다시 정리하기!
