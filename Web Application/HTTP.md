## HTTP

- HTTP method 종류를 알 수 있다.
- HTTP 구조를 이해할 수 있다.

### HTTP란?

- HyperText Transfer Protocol의 약자로 WWW상에서 정보를 주고받을 수 있는 프로토콜
- 주로 HTML문서를 주고받는 데에 사용
- 클라이언트와 서버 사이에 이루어지는 요청/응답(request/response) 프로토콜
    + 웹 브라우저가 HTTP를 통하여 서버로부터 웹페이지나 그림 정보를 요청하면, 서버는 이 요청에 응답하여 필요한 정보를 해당 사용자에게 전달

### HTTP Header 구조

#### 요청 헤더

- GET /test/test.htm HTTP /1.1
    + 요청 method, 요청 파일정보, http 버전
- Accept: 클라이언트가 허용할 수 있는 파일 형식
- User-Agent: 클라이언트 소프트웨어의 이름과 버전 등을 표시
- Host: 요청을 한 서버의 Host
- Refer: 특정 페이지에서 링크를 클릭하여 요청을 하였을 경우에 나타나는 필드로써 링크를 제공한 페이지
- Cookie: 웹 서버가 클라이언트에 쿠키를 저장해 놓았다면 해당 쿠키의 정보를 이름-값 쌍으로 웹 서버에 전송
- Accept-Language: 클라이언트가 인식할 수 있는 언어
- Accept-Encoding: 클라이언트가 인식할 수 있는 인코딩 방법
    + 서버에서 gzip, deflate로 압축한 리소스를 클라이언트가 해석 할 수 있다는 의미
    + 서버에서 압축을 했다면 Content-Encoding 헤더에 해당 압축 방법이 명시 되어 있음

#### 응답 헤더

- HTTP/1.1 200 OK
    + HTTP 버전과 응답 코드(200 성공)
- Server: 웹 서버 정보를 나타냄
- Content-Type: 요청한 파일의 MIME 타입
    + text/html은 text중 html 파일임을 나타냄
- Content-Length: 헤더 이후 이어지는 데이터의 길이(바이트 단위)


### HTTP method

#### GET vs POST

- GET은 가져오는 것, POST는 수행하는 것

#### GET

- 서버에서 어떤 데이터를 가져와서 보여주는 용도. 즉, 서버의 값이나 상태 등을 바꾸지 않음
- the query string (name/value pairs) is sent in the URL
- can be cached
- remain in the browser history
- can be bookmarked
- should never be used when dealing with sensitive data
- have length restrictions
- should be used only to retrieve data

#### POST

- 서버의 값이나 상태를 바꾸기 위해 사용
- 예를 들어 글쓰기를 하면 글의 내용이 DB에 저장이 되고, 수정을 하면 DB의 값이 수정이 됨
- never cached
- do not remain in the browser history
- cannot be bookmarked
- have no restrictions on data length



### 참고 사이트
- [HTTP 개요](https://developer.mozilla.org/ko/docs/Web/HTTP/Overview)
