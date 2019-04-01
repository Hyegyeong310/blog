---
layout: post
title: 'Sequelize로 RDS 연결'
author: HyeGyeong
categories: [2weeks-project, AWS, RDS]
image: 'assets/images/AWS-Feature.png'
---

## Sequelize로 RDS 연결

```js
// Table(user, picture, character) 생성 및 관계 설정
db.User = require(‘./users’)(sequelize, Sequelize);
db.Picture = require(‘./pictures’)(sequelize, Sequelize);
db.Character = require(‘./characters’)(sequelize, Sequelize);

// User hasMany Picture (one:User to many:Picture 관계)
db.User.hasMany(db.Picture, { foreignKey: ‘user_id’, sourceKey: ‘id’ }); // foreignKey는 여기서 생성. 미리 생성하면 이미 있는 키라서 set 불가
db.Picture.belongsTo(db.User, { foreignKey: ‘user_id’, targetKey: ‘id’ });

// User hasMany Character
db.User.hasMany(db.Character, { foreignKey: ‘user_id’, sourceKey: ‘id’ });
db.Character.belongsTo(db.User, { foreignKey: ‘user_id’, targetKey: ‘id’ });
```

## charset (utf-8) 설정

```js
// app.js
let sequelize = require('./models').sequelize;
sequelize.query('SET NAMES utf8;');
sequelize.sync(); // DB 동기화

// index.js
let sequelize = new Sequelize(
  config.database,
  config.username,
  config.password,
  config,
  {
    define: {
      // charset:'utf-8' 설정
      charset: 'utf8',
      collate: 'utf8_general_ci'
    }
  }
);

// characters.js
module.exports = (sequelize, DataTypes) => {
  return sequelize.define(
    'character',
    {
      char: {
        type: DataTypes.STRING(50),
        allowNull: true
      }
    },
    {
      // charset: 'utf-8' 설정. users.js, pictures.js도 같다.
      charset: 'utf8',
      collate: 'utf8_general_ci',
      timestamps: false
    }
  );
};
```
