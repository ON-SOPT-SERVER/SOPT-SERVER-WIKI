## S3

### Multer S3, sdk 설치

```bash
$ npm install multer-s3 aws-sdk
```

#### `modules/multer.js`

```javascript
const multer = require('multer');
const multerS3 = require('multer-s3');
const aws = require('aws-sdk');
aws.config.loadFromPath(__dirname + '/../config/s3.json');

const s3 = new aws.S3();

const upload = multer({
    storage: multerS3({
        s3,
        bucket: '<bucket name>',
        acl: 'public-read',
        key: function(req, file, cb){
            cb(null, 'images/origin/' + Date.now() + '.' + file.originalname.split('.').pop());
        }
    })
});

module.exports = upload;
```

#### `config/s3.json`

```json
{
    "accessKeyId": "s3 액세스 키 아이디",
    "secretAccessKey": "s3 시크릿 액세스 키",
    "region": "ap-northeast-2"
}
```

---

### 실습 - 클라이언트에게 s3에 저장된 사진의 url 전송하기

```javascript
const express = require('express');
const router = express.Router();
const upload = require('../../modules/multer');

router.post('/single', upload.single('image'), async (req, res) => {
   const image = req.file.location;
    console.log(req.file);
    console.log(req.body);
    res.send({
        imageUrl: image,
        file: req.file,
        body: req.body
    });
});

router.post('/array', upload.array('images', 3), async (req, res) => {
    const imageUrls = req.files.map(file => file.location);
    console.log(req.files);
    console.log(req.body);
    res.send({
        imageUrls: imageUrls,
        file: req.files,
        body: req.body
    });
});

module.exports = router;
```





