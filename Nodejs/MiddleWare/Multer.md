### 📌 Index

1. [Multer]()
2. [Multer 설치](#설치)
3. [사용법](#사용법)
4. [Multer 함수](#multer-함수들)
5. [실습](#실습)

---

## Multer✨

Multer는 파일 업로드를 위해 사용되는 `multpart/form-data`를 다루기 위한 Node.js의 미들웨어!

Multer는 multipart가 아닌 form 에서는 동작하지 않는다.

### 설치

```bash
$ npm install --save multer
```

### 사용법

Multer는 `body` 객체와 한 개의 `file` 혹은 여러 개의 `files` 객체를 `request` 객체에 추가한다.

`body` 객체는 폼 텍스트 필드의 값을 포함하고, `file` / `files` 객체는 폼을 통해 업로드 된 파일들을 포함하고 있다.

Multer는 옵션 객체를 사용할 수 있다. 그 중 가장 기본 옵션인 `dest` 요소는 Multer에게 파일을 어디로 업로드할 지를 알려준다. 만약 옵션 객체를 생략했다면, 파일은 디스크가 아니라 메모리에 저장된다.

기본적으로 Multer는 이름이 중복되는 것을 방지하기 위해서 파일의 이름을 재작성한다. 필요에 따라 해당 함수는 커스터마이징이 가능하다.

Multer로 정달 가능한 옵션들:

| Key                 | Description                                   |
| ------------------- | --------------------------------------------- |
| `dest` or `storage` | 파일이 저장될 위치                            |
| `fileFilter`        | 어떤 파일을 허용할지 제어하는 함수            |
| `limits`            | 업로드 된 데이터의 한도                       |
| `preservePath`      | 파일의 base name 대신 보존할 파일의 전체 경로 |

보통의 웹 앱에서는 `dest` 옵션 정도만 필요할지도 모른다. 설정 방법은 아래와 같다.

```javascript
var upload = multer({ dest: 'uploads/' });
```

### Multer 함수들

#### `.single(filedname)`

`fieldname` 인자에 명시된 이름의 단수 파일을 전달받는다. 👉🏻 즉, reqest 에서 key가 `fieldname` 인 요소를 업로드 해주는 것이다. 그래서 postman으로 테스트 할 때 ❗ **Multer fieldname과 이미지의 Key값**이 일치해야한다 ❗

이 파일은 `req.file` 에 저장된다😍

#### `.array(filedname[, maxCount])`

`filedname` 인자에 명시된 이름의 파일 전부를 **배열 형태**로 전달받는다. 선택적으로 `maxCount`에 병시된 값 이상의 파일이 업로드 될 경우 에러를 출력할 수 있다. 전달 된 배열 형태의 파일은 `req.files`에 저장된다.

등 많다 ! 더 상세한 건 [여기](https://github.com/expressjs/multer/blob/master/dic/README-ko.md)에서 보자

---

### 실습

1. /POST localhost:3000/multer/single
2. /POST localhost:3000/multer/array

라우팅을 구현하고 나서 로직을 실습했다.

```javascript
// routes/multer/index.js

const express = require('express');
const router = express.Router();
const multer = require('multer');
const upload = multer( { dest: 'upload/' }); // multer() 정의

...

module.exports = router;
```

#### `single(fieldname)`

```javascript
router.post('./single', upload.single('image'), async (req, res) => {
    console.log(req.file);
    console.log(req.body);
    res.send({
        imageUrl: image,
        file: req.file,
        body: req.body
    });
});
```

#### `array(filedname[, maxCount])`

```javascript
router.post('/array', upload.array('image', 3), async (req, res) => {
    console.log(req.files);
    console.log(req.body);
    res.send({
        file: req.files,
        body: req.body
    });
});
```



