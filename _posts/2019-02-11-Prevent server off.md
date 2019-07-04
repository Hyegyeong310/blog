---
layout: post
title: 'Server 꺼짐 방지'
author: HyeGyeong
categories: [2weeks-project, server, rds]
image: 'assets/images/off.jpeg'
---

## Prevent server off

- use [forever] npm package
- forever: Forever npm package

```js
// forever npm on
forever start app.js
// forever npm off
forever stop app.js
```

- 어느정도 진행한 뒤 설정하는 게 좋을 듯. 서버 구축 중에는 수정사항이 많아서 stop해야하는 상황이 계속 생김.

## sequelize 관계

```js
let db = {};
db.sequelize = sequelize;
db.Sequelize = Sequelize;

db.User = require('./user')(sequelize, Sequelize);
db.Comment = require('./comment')(sequelize, Sequelize);

// foreignKey: 외래키. Comment table's column. / sourceKey: User table's id
db.User.hasMany(db.Comment, { foreignKey: 'commenter', sourceKey: 'id' });
// foreignKey: Comment table's column. / targetKey: User table's id
db.Comment.belongsTo(db.User, { foreignKey: 'commenter', targetKey: 'id' });

module.export = db;
```

## EC2, RDS connect

- 저번 주 토요일까지는 잘 됐는데 오늘 갑자기 안 됌.
- **EC2 보안그룹 문제.**
- EC2와 RDS(VPC 보안 그룹) 서로 연결 확인해야 함.
