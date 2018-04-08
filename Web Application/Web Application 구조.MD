## Web Application 구조 및 아키텍처

### 목표

- Web Application의 전반적인 흐름에 대해 이해한다.
- Web Application을 구성하는 요소에 대해 이해한다.

### Web의 구조

- Web Server: 정적 요소 처리
- Web Application Server: 동적 요소 처리

![web 구조](http://img1.daumcdn.net/thumb/R1920x0/?fname=http%3A%2F%2Fcfile24.uf.tistory.com%2Fimage%2F257D083B594F020B2E52CC)

### Java 기반 Web Applicatoin 개발시 구조

![Java Web Application](http://img1.daumcdn.net/thumb/R1920x0/?fname=http%3A%2F%2Fcfile6.uf.tistory.com%2Fimage%2F2450AF3B594F020D228AD1)

### Web Server

- HTTP 프로토콜을 기반으로 하여, Web 클라이언트(브라우저)로 부터의 요청을 서비스 하는 기능을 담당하는 프로그램
- Apache를 많이 사용
- html, 이미지, xml 등의 정적인 요소에 대한 처리 담당

### Web Application Server

- 여러 Web 클라이언트(브라우저)의 요구를 Web 서버 혼자 감당하기 힘들기 때문에, 구조적으로 Web 서버의 기능을 분리하기 위해 만들어진 것
- Tomcat, Weblogic 등등
![was](http://cfile24.uf.tistory.com/image/156A50404F93CDE817331E)

### Web Server VS Web Application Server

- Web Server의 경우 html, 이미지들의 요청을 처리하는데 빠르고, Web Application Server는 Servlet이나, JSP의 비지니스 로직을 수행하는데 적합
- 서로 다른 강점을 합하기 위해 보통 둘 다 연동하여 서비스를 함

### 참고 사이트

- [WAS와 웹서버의 차이](https://sungbine.github.io/tech/post/2015/02/15/tomcat%EA%B3%BC%20apache%EC%9D%98%20%EC%97%B0%EB%8F%99.html)
- [Web server 및 어플리케이션 이해](http://unionbaby.tistory.com/entry/Web-server-%EB%B0%8F-%EC%96%B4%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98%EC%9D%98-%EC%9D%B4%ED%95%B4%EC%99%80-tomcat-%EA%B5%AC%EC%A1%B0)
