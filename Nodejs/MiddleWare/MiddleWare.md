## MiddleWare

### 미들웨어란

> "Middleware functions are functions that have access to the request object (req), the response object (res), and the next function in the application’s request-response cycle." - middleWare docs

서버가 요청에 대한 응답을 처리할 때, 중간에 어떠한 동작을 해주는 함수.

---

#### 우리가 보는 요청과 응답

client에서 `Request`를 보내면 Server에서 해당 클라이언트에`Response` 보냄.

끝.

#### 실제 Express에서 Request 처리 과정

**`Request 도착`** 👉🏻 `logger(morgan)` 👉🏻 `json, urlencoded` 👉🏻 `cookieParser` 👉🏻 `static` 👉🏻 `라우터` 👉🏻 `404 처리 미들웨어` 👉🏻 `에러 핸들러` 👉🏻 **`Response`**

---

`app.js`를 보면 `app.use()` 안에 있는 함수들이 바로 **미들웨어 **❗

실제로 코드를 보면`request`가 올 때마다 미들웨어를 거쳐서 `response`를 보낸다.

```javascript
//app.js
...
app.use(logger('dev'));
app.use(express.json());
app.use(express.urlencoded({ extended: false }));
app.use(cookieParser());
app.use(express.static(path.join(__dirname, 'public')));

app.use('/', indexRouter);


// catch 404 and forward to error handler
app.use(function(req, res, next) {
  next(createError(404));
});

// error handler
app.use(function(err, req, res, next) {
  // set locals, only providing error in development
  res.locals.message = err.message;
  res.locals.error = req.app.get('env') === 'development' ? err : {};

  // render the error page
  res.status(err.status || 500);
  res.render('error');
});
...
```

