## Spring Boot

### What is Spring Boot?

- 단독으로 실행이 가능하고(stand-alone), 제품 수준의(production-grade) 스프링 기반 어플리케이션을 제작하는 것을 목표로 진행된 프로젝트

### 주요 기능

- 단독 실행이 가능한 수준의 스프링 어플리케이션 제작이 가능
- 내장된 Tomcat, Jetty, UnderTow 등의 서버를 이용해서 별도의 서버를 설치하지 않고 실행이 가능
- 최대한 자동화된 설정을 제공
- XML 설정 없이 단순한 설정 방식을 제공

### Spring Boot 환경설정

- [intelliJ에 Boot 적용](https://m.blog.naver.com/PostView.nhn?blogId=togksdl92&logNo=220853513678&proxyReferer=https%3A%2F%2Fwww.google.co.kr%)
- [spring 올리기](http://projects.spring.io/spring-boot)

### 실행

- default: 임베디드 톰캣이 적용되어 있음
- 임베디드 톰켓 제외 설정을 위해 pom.xml에 아래와 같은 설정 필요
![exclusion tomcat](https://media-api.atlassian.io/file/25a6a340-2a72-4bf7-9901-0498c6890c61/image?mode=full-fit&client=ac9cd94a-a769-4dac-b7f3-e1982c424403&token=eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJhYzljZDk0YS1hNzY5LTRkYWMtYjdmMy1lMTk4MmM0MjQ0MDMiLCJhY2Nlc3MiOnsidXJuOmZpbGVzdG9yZTpmaWxlOjI1YTZhMzQwLTJhNzItNGJmNy05OTAxLTA0OThjNjg5MGM2MSI6WyJyZWFkIl19LCJleHAiOjE1MDA3NzIwMDEsIm5iZiI6MTUwMDc2ODY0MX0.01cO1MjmBpPSJxjq6I03SWwdikxl9xtPaCYMhGtn0qI)

### 빌드 결과물

- default : jar 형태로 배포 (임베디드톰캣 포함)
- war 형태로 제공하기 위해 별도 설정이 필요
    1) SpringBootApplication 의 Application class 에 SpringBootServletInitializer 를 상속(extends)
    2) pom.xml에 packaging 설정 추가
    ```
    <packaging>war</packaging>
    ```
    3) pom.xml에 dependency 설정
    ```xml
    <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-tomcat</artifactId>
       <scope>provided</scope>
    </dependency>
    ```
