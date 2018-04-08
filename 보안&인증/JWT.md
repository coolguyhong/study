## JWT란?

- party 간 정보를 안전하게 전달하기 위한 compact하고 self-contained 한 open standard(RFC 7519)
- 다양한 프로그래밍 언어에서 지원 - C, Java, Python 등등
- self-contained: 필요한 정보를 자체적으로 갖고 있음(토큰에 대한 기본정보, 전달할 정보, signature)
- 쉽게 전달 될 수 있음 - 웹서버의 경우 HTTP 헤더 또는 URL 파라미터로 전달 할 수 있음

## JWT 는 어떤 상황에서 사용될까?

- 회원 인증: 유저가 인증을 하면 JWT 토급을 발급하고 유저는 매 요청시 마다 발급받은 토큰을 전달하여 유저가 요청한 작업에 권한이 있는지 검증
- 정보 교환: 정보가 sign이 되어있기 때문에 안정성있게 정보를 교환하기에 좋은 방법


## JWT의 구조

- . 을 구분자로 3가지의 문자열로 되어있음
![jwt구조](https://velopert.com/wp-content/uploads/2016/12/jwt.png)


### 헤더(Header)

- typ: 토큰의 타입을 지정(JWT)
-  alg: 해싱 알고리즘을 지정하며 보통 HMCA SHA256 or RSA를 사용, 토큰을 검증할 때 사용되는 signature부분에서 사용
```xml
{
  "alg": "HS256",
  "typ": "JWT"
}
```

### 정보(payload)

- Payload는 클레임으로 이루어짐
- 클레임: name / value 한 쌍으로 이루어진 정보의 한 조각
- 클레임의 종류
    + registered claim
    + public claim
    + private claim
- registered claim
    + 서비스에 필요한 정보가 아닌 토큰에 대한 정보들을 담기 위한 이름이 이미 정해진 클레임
    + 사용은 선택적임
    ```xml
    {
      iss: 토큰 발급자 (issuer)
      sub: 토큰 제목 (subject)
      aud: 토큰 대상자 (audience)
      exp: 토큰의 만료시간 (expiraton), 시간은 NumericDate 형식으로 되어있어야 하며 (예: 1480849147370) 언제나 현재 시간보다 이후로 설정되어있어야합니다.
      nbf: Not Before 를 의미하며, 토큰의 활성 날짜와 비슷한 개념입니다. 여기에도 NumericDate 형식으로 날짜를 지정하며, 이 날짜가 지나기 전까지는 토큰이 처리되지 않습니다.
      iat: 토큰이 발급된 시간 (issued at), 이 값을 사용하여 토큰의 age 가 얼마나 되었는지 판단 할 수 있습니다.
      jti: JWT의 고유 식별자로서, 주로 중복적인 처리를 방지하기 위하여 사용됩니다. 일회용 토큰에 사용하면 유용합니다.
    }
    ```
- public claim
    + 충돌이 방지된 (collision-resistant) 이름을 가지고 있어야 하며, 충돌을 방지하기 위해서 클레임 이름을 URI 형식으로 짓습니다.
    ```xml
    {
        "https://velopert.com/jwt_claims/is_admin": true
    }
    ```
- private claim
    + 양 측간에 (보통 클라이언트 <->서버) 협의하에 사용되는 클레임들
    + 공개 클레임과는 달리 이름이 중복되어 충돌이 될 수 있으니 사용할때에 유의
    ```xml
    {
        "username": "velopert"
    }
    클레임셋은 암호화 되지 않음, 보안이 중요한 데이터는 포함이 되면 안됨
  인코딩 특성상 클레임셋의 내용이 많아지면 토큰의 길이가 길어짐
  토큰을 강제로 만료시킬 방법이 없음, 로그아웃 하더라도 만료시간까지 토큰이 유효함  ```
- payload 예제
```xml
{
    "iss": "velopert.com",
    "exp": "1485270000000",
    "https://velopert.com/jwt_claims/is_admin": true,
    "userId": "11028373727102",
    "username": "velopert"
}
```

## 서명(signature)

- 헤더와 정보의 인코딩 값을 합친 후 주어진 secret으로 해쉬를 하여 생성
서명생성 pseudocode
```javascript
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```
- encoded
```javascript
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
```

## JWT 사용 시 주의점

- 클레임셋은 암호화 되지 않음, 보안이 중요한 데이터는 포함이 되면 안됨
- 인코딩 특성상 클레임셋의 내용이 많아지면 토큰의 길이가 길어짐
- 토큰을 강제로 만료시킬 방법이 없음, 로그아웃 하더라도 만료시간까지 토큰이 유효함
