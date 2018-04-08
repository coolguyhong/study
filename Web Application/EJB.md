## EJB(Engerprise Java Beans)

### 개요

- 어플리케이션의 업무 로직을 가지고 있는 서버 어플리케이션

### 특징 및 도입효과

- 어플리케이션 개발 용이
- 어플리케이션 이동성
- 서버 어플리케이션을 보다 빠르게 구축 가능
- 개발의 생산성이 향상되어 개발 비용 삭감

### 기본구성

- Enterprise Bean
- Container
- EJB Server
- Client Application

#### Enterprise Bean

- 비즈니스 로직을 실장한 서버 컴포넌트
- 2가지 모델이 있음
    + Session Bean: 클라이언트의 대화처리를 실현하는 Object
    + Entity Bean: Database에 격납된 레코드를 Object로서 뽑아내거나 격밥하기 위하여 이용하는 Object
- 일반적으로 클라이언트가 Session Bean을 불러 Session Bean이 Entity Bean을 불러 DB에 접근

#### Container

- EJB서버와 Enterprise Bean의 중간에 위치해, 클라이언트 어플리케이션은 그 컨테이너를 경유해서 Enterprise Bean에 접근

#### EJB Server

- 컨테이너를 관리해서 EJB로서 필요한 시스템 레벨의 서비스(DB 처리, 트랜젝션 처리)등을 실현

#### Client Application

- EJB에 준거한 클라이언트 어플리케이션
- Java Applet, Java Application, Servlet, Java Server Pages(JSP) 베이스의 어플리케이션 등

### 참고 사이트

- [EJB란?](http://pokey.tistory.com/7)
