## OpenID

### 개요

- OpenID 는 사용자 중심 identity 를 위한 분산형 공개 표준 기술
- OpenID 는 하나의 URI로 자신을 식별하도록 함

### OpenID 에 사용되는 기본 용어들

- 최종 사용자 (end user): 자신의 identity를 어떤 사이트에 밝히고자 하는 사람.
- ID (identifier): 최종 사용자가 그들의 OpenID 아이디로 선택한 URL 이나 XRI.
- ID 제공자 (identity provider): OpenID URL 또는 XRI 등록을 제공하고 OpenID 인증 (추가적으로 다른 identity 서비스도) 을 제공하는 서비스 제공자.
- relying party: 최종 사용자의 ID를 검증하고자 하는 사이트.
- server 또는 server-agent: 최종 사용자의 ID를 검증해주는 서버로, 최종 사용자의 자체 서버 (블로그 등) 또는 ID 제공자에 의해 운영되는 서버가 될 수 있다.
- user-agent: 최종 사용자가 ID 제공자나 relying party에 접속할 때 사용하는 (브라우저 등) 프로그램.

### Process

![Process](https://www.ibm.com/developerworks/mydeveloperworks/blogs/48a78681-82cc-434f-9c78-3e9117bfd466/resource/BLOGS_UPLOADED_IMAGES/OpenID_Auth_Flow.JPG)

- Alice는 RP 사이트(example.com)에 접속한다.
- Alice는 RP 사이트에 자신의 ID(alice.openid-provider.org)를 입력한다.
- RP는 ID가 URL임을 확인하고 이 URL이 가리키는 웹페이지를 요청
- RP는 ID 제공자와 통산하는 두 가지 모드가 있다.
    + checkid_immediate: 사용자 간섭없이 두 서버간의 통신으로 처리
    + checkid_setup: 사용자가 직접 웹브라우저를 통해서 ID 제공자 서버와 통신을 하여 RP로 접속한다.
- checkid_immediate 모드일 경우 RP는 shared secret를 ID제공자 서버로부터 받아 저장한 후 처리된다.
- checkid_setup의 경우, RP는 사용자의 브라우저를 ID 제공자 서버페이지로 redirect한다.
- ID 제공자 서버는 패스워드를 통한 인증을 수행하며, RP에게 사용자의 세부정보를 허락한 것인지를 사용자에게 묻는 과정이 진행된다.
- 인증이 성공하면, 사용자의 브라우저는 인증정보와 함께 RP 사이트로 redirect 된다.
- RP는 해당 인증정보가 ID 제공자로부터 발급된건지 확인할 필요가 있다.
    + shared secret를 가지고 있을 경우 직접 유효검증을 수행한다.
    + 존재하지 않을 경우, background request(check_authentication) 을 통해 검증을 수행해야 한다.

![OpenID 1.1 Protocol Flow](https://blog.outsider.ne.kr/attach/1/1378459974.png)
