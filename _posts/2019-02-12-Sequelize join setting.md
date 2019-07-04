---
layout: post
title: 'S3로 file upload'
author: HyeGyeong
categories: [2weeks-project, S3, rds]
image: 'assets/images/react-s3.png'
---

## Sequelize join table setting

- Get /api/user 에서 user table 외에 interest, pictures table join해서 보여줌.

```js
// GET /api/users
app.get('/api/users', (req, res) =>
  User.findAll({
    include: [{ model: Interest }, { model: Picture }]
  })
    .then(users => {
      res.json(users);
      res.end();
    })
    .catch(err => console.log('Error: ', err))
);
```

## 오늘도 RDS 문제 터짐.

- config folder는 숨겨야 하는 폴더인데 .gitignore에 추가 안 함. 즉, secret key들을 모두 github에 공개하고 있었다는 얘기.... 앞으로 작업할 때 꼭 체크 할 것!

- 기존 config 폴더에 있던 secret key를 수정했는데 RDS가 연결되지 않음. 역시나 localhost에서는 원하는 대로 잘 불려짐. 보안 그룹 문제.

- **보안 그룹 재설정**, **포트번호**, 비밀번호, 주소 등 싹 고치고 나니 다시 잘 돌아가는 중

## S3 Connect

- 'aws-sdk', 'multer', 'multerS3' module 이용해서 연결

```js
// aws s3 connect
let AWS = require('aws-sdk');
AWS.config.loadFromPath( // 파일 루트 설정한 후 확인 필수!
  path.join(__dirname, '..', '/server/config', 'awsconfig.json')
);
let s3 = new AWS.S3();
let multer = require('multer');
let multerS3 = require('multer-s3'); // s3 file upload를 도와줌.
let upload = multer({ // multer setting
  storage: multerS3({
    s3: s3,
    bucket: 'hoa-hoa-project',
    key: (req, file, cb) => {
      let extension = path.extname(file.originalname);
      cb(null, Date.now().toString() + extension);
    },
    acl: 'public-read-write'
  }),
  limits: { fileSize: 5 * 1024 * 1024 } // 올릴 수 있는 사이즈 제한
});

// upload type setting
let type = upload.single('file');
app.post('/api/upload', type, (req, res, next) => {
  let imgFile = req.file;
  res.json(imgFile);
});

// if status(200)
{
    "fieldname": "file",
    "originalname": "file.gif",
    "encoding": "7bit",
    "mimetype": "image/gif",
    "size": 147645,
    "bucket": "Your bucket name",
    "key": "changed file name",
    "acl": "public-read-write",
    "contentType": "application/octet-stream",
    "contentDisposition": null,
    "storageClass": "STANDARD",
    "serverSideEncryption": null,
    "metadata": null,
    "location": "Your S3 address/changed file name",
    "etag": "\"암호화된 코드\""
}
```
