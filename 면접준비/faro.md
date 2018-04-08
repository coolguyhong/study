## FARO 이력검증

### 내가 한 것

- byte길이 check 공통유틸 구현
    + validationCheck.js textLengthByte()

- 패키지 구조 변경 기획
    + 규칙 없이 모듈들이 결합된 상태로 코드 개발이 진행됨
    + core 부분을 제외한 부분들 중 대부분을 plugin 형태로 분리해 내기 위해 패키지 정비

- Multi Language 개선을 위한 설계
- Java Linting Tool Research
    + Checkstyle과 PMD를 통해 적용
    + checkstyle: 코딩 스타일 검사 도구. 정렬을 비롯하여 말 그대로 스타일을 검증하는 데에 이용. config 파일을 통해 원하는 스타일을 설정하고 있으며 github를 통해 구글 기본 스타일 config를 배포하고 있음
    + PMD: 정적 검사 도구의 대표적인 툴. 컴파일 전 가상문맥트리를 구성하여 이를 통해 발생할 수 있는 오류나 예외에 대해 알려줌. 또한 순환복잡도에 대한 검사도 가능
    + FindBugs: PMD와 기본 개념은 비슷하지만, 컴파일 후의 코드를 통해서 잠재 오류를 찾아내는 것이 특징. 멀티스레드 환경에서의 테스트가 필요하지 않으면 PMD를 이용. 필요하다면 PMD와 FindBugs를 함께 이용하는 것이 일반적

- CollaboZone H2버전 Anyframe Admin Portal 설치
    + ubuntu 환경에 java1.7 설치 및 java_home 설정 잡음
    + tomcat 설치
    + admin portal war파일 풀어서 배포

- 보안관련 이슈
    + xss 보안 취약점 해결(Lucy xss filter 적용)
        - xssfilter.java / servletRequestwrapper.java
    + 암호화 알고리즘 sha1 알고리즘과 salt를 적용하여 비밀번호 암호화 기능 강화

  - 관리자 IP에 대해 asterisk 문자 허용

  - 로그인 이력 테이블 로그 채번시 문제됨
     + LOG_SQ 채번 방식이 MAX + 1 형태로 되어 있음
     + 과부하 테스트시 transaction이 동시에 여러 건이 발생: 현재 형태의 경우 +1 형태로 채번을 할 경우 Key 값인 LOG_SQ가 겹칠 수 있음
     + UUID이용하여 key값 채번
     + UUID란 범용 고유 번호(Universally Unique Identifiers)라고 불리며 128비트의 숫자들을 조합
     + DB저장시 -는 제거: UUID 자체가 32개의 16진수로 표현된 128비트의 고유 식별자 이며, -자체는 가독성을 위함. DB insert시 불필요한 저장공간 낭비 초래

  - 깃브랜칭 전략 도입
      + 소프트웨어 버전 표기법 정의

  - 사용자별 메뉴 접근 이력 기능 문의
      + http 요청 쿼리에 menuSQ가 있음 이점에 착안하여 Interceptor를 통해 was 부분으로 전달되는 http요청을 캐치하고 query에 menuSq 항목과 그 값이 존재하는지 확인 후, 현재 접속 중인 유저 정보와 함께 로그를 남김
      + Interceptor 설정부: dispatcher-servlet.xml
      + MenuLogInterceptor.java

  - 로그인 이후 리다이렉트할 URI 설정
      + 설정에 redirect URL 설정 추가

  - 세션 처리 후 문제 발생
      + ![스프링 익셉션](springboot.tistory.com/25)
      + exception 처리 handler 해결
      + 발생 원인
          - 화면과 서버 사이, 전달값에 대한 타입이 다름
          - 화면: Ajax수행(JSON으로 요청 후, JSON값으로 반환을 기대함)
          - 서버: ModelAndView를 이용하여 jsp 반환
      + 해결방향
          - 예외 발생 시, 요청에 맞는 적절한 response 제공 필요
      + Client에서 서버로 요청하는 경우
          - lego_common_ajax
          - aui gird
          - app.js의 Ajax
          - 세션 만료 후 또는 권한 없는 사용자가 팝업 호출할 경우

      + 메시지 아키텍처가 자바의 예외 처리 과정을 포함하여 설계되어 있는 탓에 세션 메시지만을 위한 별도 처리 불가능하여 기존의 자바 예외 처리 과정을 살펴야 했음

      + 이후 예외 처리 자체에 대한 세밀한 분석 과정 결과 전제로 삼아야 할 것들을 정함
      + 클라이언트에서는 일반적이고 일관적인 HTTP 요청/응답 처리가 이루어저야 함
          - 브라우저를 통해 보여지는 UI는 HTTP 요청과 응답을 처리하기 위해 존재
      + HTTP 요청에 따른 응답에서 상태를 표현하기 위한 필드가 이미 존재
          - HTTP 상태코드로 표현 가능한 예외 경우
              + 401: 인증안됨(세션 중복세션 등등)
              + 403: 권한
              + 404: 권한이 없는 리소스 요청, 서버에서 처리하지 않은 리소스
              + 500: 그외 예외
      + 서버에서는 모든 요청에 대해 특수한 경우 없이 일관적으로 답해야 함
          - 모든 요청은 ajax 여부에 따라 둘로 나눌 수 있으며 이에 따른 http 본문의 형식은 달라질 수 있음

      + 정적 자원
          - web.xml에 기술된 error 처리 페이지 지정에 따른 처리
      + 동적 자원
          - 인증: applicationContext-Security.xml
          - 허가: 403은 AccessDeniedHandler 인터페이스 구현
          - 404 처리는 spring security filter를 감쌀 수 있는 별도 filter를 작성하여 처리
          - ajax: spring 에서 제공하는 handlerExceptionResolver 인터페이스를 구현하여 처리
          - 기존 auiExceptionresolver 처리하던 내용 확인 필요
          - spring context를 사용할 수 없는 경우 error 페이지로 redirect를 통해 처리

      + AUI가 HTTP의 본문의 형식을 강제하면서 야기되는 것들이 있었으며, 이를 조치하기 위한 처리에서 잘못이 있었음
         -
      + json으로 응답해야 하는 경우 aui 응답 형식으로
      + object mapper를 새로 작성
      + auimessageconverter를 wrapping 함
      + aui 요청이면 auihttpmessageconverter에서 그렇지 않으면 상속받은 부모 클래스에서 처리
      + exceptionresolver 새로 작성
          - ajax 요청이면 json형태로, 그렇지 않으면 html형태로 본문 반환 json형태는 aui 규격을 따름


### 현재 faro 권한관리 체계 정리

- 업무그룹
    + 업무그룹에 사용자가 접근 가능한 메뉴 및 메뉴에서의 수행가능한 권한 설정
    + 업무그룹에 사용자를 매핑

- 역할
    + 역할에 사용자를 매핑
    + 역할에 업무그룹을 매핑

- 리소스에 관한 권한
    + 화면은 READ_YN
    + 입력, 수정, 삭제 UPDATE_YN
    + 조회 EXECUTE_YN

- 최종적으로 업무그룹을 통해 사용자의 권한을 확인

### log 및 메시지 처리관련

- AOP를 활용하여 log 저장
    + 로그인 성공, 실패, impersonate 이력,
- 업무에 관한 로그: filter를 두어 업무 저장 또는 삭제에 관한 정보 로그에 쌓음
- 메뉴접속 이력
    + http 요청 쿼리에 menuSQ가 있음 이점에 착안하여 Interceptor를 통해 was 부분으로 전달되는 http요청을 캐치하고 query에 menuSq 항목과 그 값이 존재하는지 확인 후, 현재 접속 중인 유저 정보와 함께 로그를 남김
    + Interceptor 설정부: dispatcher-servlet.xml
    + MenuLogInterceptor.java

- DB에 메시지 관련 코드를 넣어서 관리를 하였고, i18n도움 설정을 통해 다국어 처리를 함
    + 다국어 처리를 위해서는 locale 정보를 받아와야 하는데 기본적으로 서버에서 받아오는 languae 정보로 함

### AUI관련


### Exception 처리
