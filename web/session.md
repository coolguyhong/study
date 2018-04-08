## session

### 개요

- 서버가 해당서버로 접근한 클라이언트를 식별하는 방법
- 일반적으로, 세션은 컴퓨터 시스템의 관리자(또는 OS 또는 서버)가 자신의 자산을 이용하는것을 허락한 사용자 (컴퓨팅)를 인식한 일정한 기간을 가리키는것으로 광범위하게 이해

### HTTP

- 모든 사용자에 대해 TCP 연결유지 하지 않음
- 이러한 Stateless 특성때문에 서로 다른 request(ex, 첫번째와 두번째 request)에 대해 같은 요청자라고 판단할 수 없음

### Cookie

- Http Header Reserved Field 중 하나

#### Attributes

- Domain and Path: Scope 를 정의. 클라이언트는 해당 Domain 과 Path가 매칭될때만 해당 Cookie를 보내게 된다.
- Expires and Max-Age
    + Cookie 의 만료시간을 설정.
    + 만료정보가 포함되지 않으면, Session Cookie 로 간주되어 메모리에 저장되며 디스크에 기록되지 않음 (브라우저 종료시 영구 손실)
- Secure: Secure 통신이 아닌경우 Cookie 를 전송하지 않도록 한다.
- HttpOnly
    + http 및 https 통신 이외에서는 해당 값이 보이지 않도록 한다.
    + client-side scripting languages(Javascript...) 에서 해당 Cookie 값에 접근할 수 없도록 한다.

#### Cookie 생성

- Response 중 Set-Cookie 라는 이름의 Header 로 사용된다.

```xml
HTTP/1.0 200 OK
Content-type: text/html
Set-Cookie: yummy_cookie=choco
Set-Cookie: tasty_cookie=strawberry
```

#### Cookie 사용

- Set-Cookie에 의해 생성된 정보를 Client는 다음 요청시 같은 Domain 및 하위 path에 대해 포함하여 보내야 한다.
- Protocol 에 의해 정의 되는 규약이므로, 어플리케이션의 구현없이 브라우저에 의해 동작이 된다.
- 일반적으로 알려진 서버별 쿠키명: JSESSIONID (JSP), PHPSESSID (PHP), CGISESSID (CGI), ASPSESSIONID (ASP)

```xml
GET /sample_page.html HTTP/1.1
Host: www.example.org
Cookie: yummy_cookie=choco; tasty_cookie=strawberry; JSESSIONID=xxxxxxxxxxxxxxxxxx
```

### Process

- 클라이언트는 abc.com 에 접속한다.
- 클라이언트는 로그인 페이지에서 로그인을 수행한다.
- 서버는 로그인정보가 유효하면, 서버내에 사용자정보를 저장하고 Cookie를 통해 유효한 Session ID를 발급한다.
- 클라이언트는 다음요청시 부터 해당 Session ID 를 Cookie 로 포함하여 함께 전송한다.
