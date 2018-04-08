## OAuth

### OAuth의 탄생과 사용

- 2007년 OAuth 1.0이 최초로 만들어짐
- 2008년 보안 문제를 해결한 수정 버전인 OAuth 1.0 revision A 나옴(OAuth 1.0a)
- 2010년 IETF OAuth 워킹그룹에 의해 이 프로토콜이 IETF 표준 프로토콜로 발표
- 2012년 OAuth 2.0 프로토콜 발표(1.0a 와 호환되지 않음)

### OAuth 1.0, 2.0 용어 비교

| 단어 | 1.0 | 2.0 |
| ---- | ---- | ---- |
| 사용자 | User | Resource Owner |
| Client | Consumer | Client |
| API 서버 | Service Provider | Resource Server |
| 인증/인가 서버 | Service Provider | Authorization Server |

### 두 가지 유형의 클라이언트와 동작 흐름

- 인가 코드 그랜트(Authorization Code Grant):신뢰 클라이언트, 서버 사이드 플로우
![인가 코드 그랜트 플로우](http://image.itmedia.co.jp/ait/articles/1209/10/mt_digid02zu01.jpg)

- 비인가 그랜트(Implicit Grant): 비신뢰 클라이언트, 클라이언트 사이드 플로우
![비인가 그랜트 프롤우](http://image.itmedia.co.jp/ait/articles/1209/10/mt_digid02zud02.jpg)

### OAuth 2.0 구현의 네 개의 단계

1. 클라이언트 애플리케이션 등록
- Client가 OAuth 2.0을 지원하는 서비스 제공자에 등록 과정 필요
- 등록 시 발급받는 항목(필수)과 입력하는 항목(서비스 제공자에 따라 다름)
    + 클라이언트 ID (필수)
    + 클라이언트 시크릿 (필수)
    + 리다이렉션 엔드포인트
    + 인가 엔드 포인트
    + 토큰 엔드 포인트

2. 액세스 토큰 얻기
- 클라이언트 유형에 따른 워크플로우 이용
- 액세스 토큰, 리프레시 토큰(옵션)을 얻음

3. 액세스 토큰 사용
- header field로 전달
    + GET
    + Authorization: Bearer [access token]
- 인코딩된 폼의 파라미터로 전달
    + POST
    + content-type: x-www-form-urlencoded
    + access_token=[access token]
- URI 질의 파라미터로 전달 (비추, 개발시 디버깅 용도로만 사용)
    + GET
    + access_token=[access token]

4. 액세스 토큰 갱신(선택)
- 인가 코드 그랜트(Authorization Code Grant) 일 때만 사용 가능
- 액세스 토큰을 얻을 때 갱신용 토큰을 같이 발급 받음
- 갱신용 토큰으로 서비스 제공자에게 갱신 요청을 하면 새로운 액세스 토큰과 또 다른 갱신용 토큰을 발급 받음

### 클라이언트 사이드 액세스 토큰 얻기(상세)

1. 인가 요청(클라이언트 → 서비스 제공자)
- GET
- url-encoded 포멧 & 파라미터
- response_type=token
- client_id=[서비스 제공자가 발급한 클라이언트 ID]
- redirect_url=[인가가 되었을 때의 리다이렉트 url] (선택)
- scope=[서비스 제공자에 의해 정의된 접근 권한 목록] (선택)
- state=[클라이언트의 요청과 그에 따른 콜백 간의 상태를 유지하기 위해 사용] (선택)

2. 인가 응답(서비스 제공자 → 클라이언트)
- url-encoded 포멧 & 프래그먼트(브라우저에서만 처리되기 때문에, 캐시되지 않기 때문에)
- access_token=[access token]
- token_type=bearer (선택) 거의 이 값을 사용
- expires_in=[토큰의 유효기간(초단위)] (선택)
- scope=[인가된 접근 권한 목록] (조건부 선택)
- state=[클라이언트에서 넘겨준 state] (선택)

### 서버 사이드 액세스 토큰 얻기(상세)

1. 인가 요청(클라이언트 → 서비스 제공자)
- GET
- url-encoded 포멧 & 파라미터
- response_type=code
- client_id=[서비스 제공자가 발급한 클라이언트 ID]
- redirect_url=[인가가 되었을 때의 리다이렉트 url] (선택)
- scope=[서비스 제공자에 의해 정의된 접근 권한 목록] (선택)
- state=[클라이언트의 요청과 그에 따른 콜백 간의 상태를 유지하기 위해 사용] (선택)

2. 인가 응답(서비스 제공자 → 클라이언트)
- url-encoded 포멧 & 파라미터
- code=[code]
- state=[클라이언트에서 넘겨준 state] (선택)

3. 액세스 토큰 요청
- POST
- Header: Authorization: Basic [client_id]:[client_secret] (BASE64 Encoded)
- grant_type=authorization_code
- code=[code]
- client_id=[서비스 제공자가 발급한 클라이언트 ID]
- redirect_url=[인가가 되었을 때의 리다이렉트 url] (선택)

4. 액세스 토큰 응답
- JSON
- access_token
- token_type
- expires_in
- refresh_token
