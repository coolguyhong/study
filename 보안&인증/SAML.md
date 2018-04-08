## SAML

### 개요

- Security Assertion Markup Language
- 인증정보 제공자와 서비스 제공자 간의 인증 및 인가 데이터를 교환하기 위한 XML 기반의 개방형 표준 데이터 포맷

### 목적

- Web Browser Single sign-on (가장 주된 목적)
- 암호 피로 감소
- 인증 위임

### Process

![Process](http://cfile25.uf.tistory.com/image/24058D43573DE1C8344D10)

- 2번 과정의 인증요청 메시지
    + xml 형태로 작성
    + AssertionConsumerServiceURL 등을 포함
    + [참고사이트](https://www.samltool.com/generic_sso_req.php)
- 6번 과정의 메시지
    + 인증성공시 AssertionConsumerServiceURL로 Assertion 을 전달하도록 처리됨
    + 인증제공자의 인증서를 통해 서명 및 암호화 된다.
    + [참고사이트](https://www.samltool.com/generic_sso_res.php)

### Prerequisite

- IdP와 SP간 프로비저닝 과정에서 인증서와 메타데이터를 교환하여 CoT(Circle of Trust) 를 설립
- 실제 교환은 관리자에 의해 수동으로 (Copy & Paste)으로 전달되는 가장 확실한 방식을 주로 사용
