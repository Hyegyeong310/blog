---
layout: post
title: 'Sequelize delete data'
author: HyeGyeong
categories: [2weeks-project, sequelize]
image: 'assets/images/delete.jpeg'
---

## Sequelize delete data

```js
// Interest table에서 user_id가 id인 data 삭제
let id = req.params.id;
Interest.destroy({ where: { user_id: id } });
```

## post data 형식이 Array일 때

```js
// Client request
{
	"interest": ["movie", "music", "game"]
}

// Server response
let body = JSON.parse(req.body.interest); // JSON.parse로 Array 형태의 Text를 Array로 바꿔줌
for (let i = 0; i < body.length; i++) {
    Interest.create({ keyword: body[i], user_id: id }); // for문을 돌면서 Interest table에 data 생성
  }
```
