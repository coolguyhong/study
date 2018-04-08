## HTTP

- HTTP 개념 및 특징에 대해 알 수 있다.

### HTTP란?

- HTTP(Hypertext Transfer Protocol)하이퍼텍스트 전송 규약
- Web-Browser(브라우저)같은 응용프로그램을 통해 Web-Client(사용자)와 Web-Server(서비스제공자)사이 데이터를 전송하는 프로토콜입니다.


### HTTP 특징

- TCP/IP를 이용하는 응용 프로토콜
    + 컴퓨터와 컴퓨터 사이 데이터를 전송 할 수 있는 장치
    + 주로 인터넷이라는 거대한 통신망을 통해 데이터를 주고 받는 응용 프로토콜

- 연결 상태를 유지하지 않는 프로토콜
    + Web-Client의 요청에 대한 응답 완료 후 연결을 종료함
    + 연결이 지속적이지 않기 때문에 추가적인 Web-Client의 요청시 어떤 Web-Client의 요청인지 모르는 단점이 존재
    + 이러한 단점을 해소하기 위해 Cookie, Session, URL ReWrigin, Hidden Form Field등을 활용

- 연결 상태를 유지하지 않기 때문에 요청/응답(request/response)방식으로 동작
