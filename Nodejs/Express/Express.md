# Express

## 📌 Index

1. [Express 프로젝트 구조](#express-프로젝트-구조) 😉
2. [Express 프로젝트 생성](#express-프로젝트-생성) 👍🏻

## Express 프로젝트 구조

### bin/www

- `app.js` (express 설정파일) 을 가져와서 HTTP 객체와 연결시키는 작업을 함.

- 서버를 구동 => `bin/www`를 실행하는 것

- 이 파일에서 포트번호를 바꿀 수 있다.

  ```javascript
  ...
  var port = normalizePort(process.env.PORT || '3000'); //포트번호
  app.set('port', port);
  ...
  ```

---

### node_modules

모듈을 설치하면 이곳에 저장된다.

---

### Public

이미지, css, js 파일들을 저장하는 곳 

---

### ✨Routes✨

라우팅을 위한 폴더, **리소스** 별로 라우팅을 구현

---

### Views

- Jade, ejs, numjucks와 같은 템플릿 엔진들을 모아두는 곳

- 웹 서버 사용시 해당 폴더의 파일들을 사용해서 렌더링

- 우리는 안 쓴다! (웹 파트에서 템플릿엔진을 사용하지 않음)

---

### ✨app.js✨

- 프로젝트의 중심
- 미들웨어 관리가 이루어짐
- 라우팅의 시작점

---

### package.json

프로젝트의 정보를 정의하고, 의존하는 패키지 정보를 명시하는 파일

```javascript
{
  "name": "myProject",
  "version": "0.0.0",
  "private": true,
  "scripts": {
    "start": "node ./bin/www"
  },
  "dependencies": {
    "cookie-parser": "^1.4.5",
    "debug": "~2.6.9",
    "express": "~4.16.1",
    "http-errors": "~1.6.3",
    "jade": "^1.11.0",
    "morgan": "^1.9.1",
    "promise-mysql": "^4.1.4"
  }
}
```

---



## Express 프로젝트 생성

1. VSCode 실행

2. 내장 터미널을 이용해서 프로젝트를 만들 위치로 이동

3. `npm install` 을 사용해서 `express`와 `express-generator`를 설치

   ```bash
   $ npm install -g express express-generator
   ```

   - `express-generator`: Express 프로젝트 생성기

   - -g 옵션: global, 컴퓨터 환경 전역에 install하기 위한 옵션

4. `express` command을 사용해서 프로젝트 생성

   ```bash
   $ express [프로젝트 이름]
   ```

5. `npm intall` 로 package.json 파일에 명시된 모듈들을 설치

   ```bash
   $ npm install
   ```

   - 프로젝트 최상위 디렉토리 안에서 실행

### 실행

npm 사용

```bash
$ npm start
```

nodemon 사용 - 실행 중에 프로젝트 파일이 변경되면 자동으로 재시작

```bash
$ nodemon start
```



