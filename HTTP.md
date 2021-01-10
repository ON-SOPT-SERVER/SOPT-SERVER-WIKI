## HTTP

### 📌 Index

1. [HTTP란?](#http란?)
2. [HTTP로 데이터를 전송하는 방법](#http로-데이터를-전송하는-방법)

---

### HTTP란?

웹에서 클라이언트와 서버가 데이터를 주고받을 수 있는 프로토콜.

프로토콜은 규칙/규약을 의미하고, 이런 프로토콜이 있어서 웹에서 이 규칙에 맞춰 정보를 교환할 수 있다.

### HTTP로 데이터를 전송하는 방법

1. URL: URL안에 정보를 넣는 두 가지 방법
   - Param: https://localhost:3000/news/23 -> 23이 뉴스의 아이디
   - Query: https://localhost:3000/news?category=society ->카테고리가 사회인 뉴스를 요청
2. HTTP header: 부가적인 정보(토큰, 쿠키 등)을 포함시킨다.
3. Body: XML, Json, Multi Form 등의 데이터를 포함시킨다.

#### HTTP Method

: HTTP의 **Request**의 형태

| Method | Action | Request Body |
| ------ | ------ | ------------ |
| POST   | Create | O            |
| GET    | Read   | X            |
| PUT    | Update | O            |
| DELETE | Delete | X            |

#### Status Code

: HTTP **Response**의 상태!

< 자주 사용되는 코드 >

| 응답 코드 |                       | 표시 상태                            |
| --------- | --------------------- | ------------------------------------ |
| 200       | OK                    | 성공                                 |
| 204       | No Content            | 성공, 전달해줄 응답 데이터는 없음    |
| 304       | Not modified          | 캐시 목적 요청 이후 수정된 것이 없음 |
| 400       | Bad Request           | 서버가 요청을 이해하지 못함          |
| 401       | Unauthorized          | 인증이 필요                          |
| 404       | Not Found             | 페이지 리소스를 찾을 수 없음         |
| 500       | Internal server error | 서버 내부 오류                       |

