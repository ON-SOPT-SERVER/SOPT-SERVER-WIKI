## Routing

### Index

1. [라우팅이란](#라우팅이란)
2. [URI 예시](#uri-예시)
3. [라우팅 예시](#라우팅-예시)

---

### 라우팅이란

URI 및 특정한 HTTP 요청 메소드 로 정해진 **특정 엔드포인트**에 대해서, 클라이언트 요청에 애플리케이션이 응답하는 방법을 결정하는 것을 뜻한다.

라우팅이 편리한 것이 Express의 장점 중 하나다.

---

### URI 예시

```
https://news.daum.net/society  # 사회뉴스
https://news.daum.net/politics # 정치뉴스
https://news.daum.net/economic # 경제뉴스
```

```
https://news.daum.net/ranking/popular # 랭킹/인기순
https://news.daum.net/ranking/bestreply #랭킹/댓글순
https://news.daum.net/ranking/age #랭킹/연령별
```

---

### 라우팅 예시

```javascript
router.METHOD('path', (req, res) => { /* logic */ });
```

METHOD 는 HTTP 요청 메소드를 쓰면 되고, 'path'에는 URI를 쓰면 된다.

---

### 라우팅 실습

#### 1. 초기 세팅에서 usersRouter 제거

프로젝트를 생성하면 `app.js`에는 `routes/index`와 `routes/users` 두개의 라우터가 존재한다 ❗ 세미나에서는 모든 라우팅 미들웨어를 `routes/index`에서 관리하기 위해 `usersRouter`를 지웠다 🤗

`app.js`에서 8번째줄과 23번째 줄을 지운다!

```javascript
...
var usersRouter = require('./routes/users'); //삭제
...
app.use('/users', usersRouter); //삭제
...
```

#### 2. 라우팅 (routes/index.js)

```javascript
//routes/index.js
const express = require('express');
const router = express.Router();

router.get('/board', function(req, res) {
	res.status(200).send('GET Method!');
});

router.post('/board', function(req, res) {
	const { title, condtent } = req.body;
	res.status(200).send('POST Method!');
});

router.delete('/board/:idx', function(req, res) {
	const boardIdx = req.params.idx;
	res.status(200).send('DELETE Method!');
});

router.put('board/:idx', function(req, res) {
	const boardIdx = req.params.idx;
	res.status(200).send('Put Method!');
});

module.exports = router; // 내보내기
```

#### 3. Postman으로 요청/응답 실습

postman으로 라우팅이 잘 됐는지, 우리가 직접 테스트해볼 수 있다 🏃🏻‍♂️