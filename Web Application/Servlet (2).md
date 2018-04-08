## Servelt


### Servlet이란?

- 클라이언트 요청을 처리하고 그 결과를 다시 클라이언트에게 전송하는 Servlet 클래스의 구현 규칙을 지킨 자바 프로그램


### Servlet 특징

- 동적 웹어플리케이션 컴포넌트
- .java 확장자
- 클라이언트의 요청에 동적으로 작동하고, 응답은 html을 이용
- java thread이용하여 동작
- MVC 패턴에서 Controller로 이용


### Servlet Container

- Servlet을 관리하는 역할
- Servlet 생명 주기를 관리하여 요청에 따른 스레드를 생성
- 클라이언트의 Request를 받아주고 Response를 보낼 수 있게 웹 서버와 소켓을 만들어 통신
    + Tomcat이 가장 대중적

### Servlet Container 역할

- 통신지원
    + 서블릿과 웹 서버가 통신할 수 있는 손쉬운 방법을 제공
    + 소켓을 만들어 통신하도록 해줌
- 생명주기 관리
    + 서블릿 컨테이너가 기동되는 순간 서블릿 클래스를 로딩해서 인스턴스화하고, 초기화 메서드를 호출하고, 요청이 들어오면 적절한 서블릿 메소드를 찾아서 호출한다. 만약 서블릿의 생명이 다하는 순간 가비지 컬렉션을 진행한다.
- 멀티쓰레딩 관리
    + 서블릿 컨테이너는 해당 서블릿의 요청이 들어오면 스레드를 생성해서 작업을 수행한다. 즉 동시의 여러 요청이 들어온다면 멀티스레딩 환경으로 동시다발적인 작업을 관리한다.
- 선언적인 보안관리
    + 서블릿 컨테이너는 보안 관련된 기능을 지원한다. 따라서 서블릿 코드 안에 보안 관련된 메소드를 구현하지 않아도 된다.
- JSP 지원


### Servlet 동작과정

![Servlet 동작과정](Servlet_동작과정.jpg)

- Servlet Container는 HttpServletRequest, HttpServletResponse 두 객체를 생성
- 사용자가 요청한 URL을 분석하여 어느 서블릿에 대한 요청인지 찾는다
- 컨테이너는 서블릿 service() 메소드를 호출하며, POST, GET 여부에 따라 doGet() 또는 doPost()가 호출된다.
- 응답이 완료되면 HttpServletRequest, HttpServletResponse 두 객체를 소멸시킨다


### 참고사이트

- [Servlet이란?](http://til0804.tistory.com/25)
