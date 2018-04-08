## REST API 개념

### API(Application Programming Interface)란??

- 응용 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스
- 예를 들어 회사에서 사용하려고 파일 제어(관리)하는 응용프로그램을 사용하려 할 때, 외부 사용자가 해당 소스 및 데이터베이스에 접근하면 안됨.
- 이런 문제를 해결하기 위해서 API가 사용 됨
- API를 통해 소스 및 데이터베이스는 접근하지 못하게 하고, 해당 프로그램을 사용할 수 있도록 기능을 제공하는 것
- 웹 API는 웹 어플리케이션 개발에서 다른 서비스에 요청을 보내고 응답을 받기 위해 정의된 명세를 일컬음

### REST API란??

- 웹의 장점을 최대한 활용할 수 있는 아키텍처로
- Representational State Transfer(표현 상태 전이, REST)
- REST API는 크게 리소스, 메서드, 메세지로 이루어짐
- "이름이 Terry인 사용자를 생성한다"
    - 리소스: "사용자" -> http://myweb/users라는 형태의 URI
    - 행위(메서드): "생성한다"라는 행위 -> HTTP POST 메서드
    - 표헌(메세지): "이름이 Terry인 사용자" -> 생성하고자 하는 사용자의 디테일한 내용은 JSON 문서를 이용해서 표현

### REST Architecture 6가지 원칙(RESTful)

- 균일한 인터페이스 Uniform Interface
- 상태없음 Stateless
- 캐시 Cache
- 클라이언트/서버 Client/Server
- 계층 시스템 Layered System
- Self-descriptiveness (자체 표현 구조)

### URI

- REST API는 리소스를 나타낼 때 URI(Uniform Resource Identifier)를 사용

#### URI 형태

- 슬래시(/)는 계층 관계를 나타내는데 사용
- URI 경로 마지막에 있는 슬래시는 아무런 의미가 없지만, 혼란을 방지하기 위해 REST API의 마지막 글자에 슬래시를 포함하면 안됨.(많은 웹 컴포넌트와 프레임워크에서는 같은 것으로 취급)
- 하이픈(-)은 URI 가독성을 높이는데 사용
    - URI를 쉽게 이해하기 위해 긴 URI에 하이픈을 사용해 가독성을 높일 수 있다.
- 밑줄은 사용하지 않는다. 대신에 하이픈(-)을 사용한다.
- URI는 소문자로 구성하는게 적합하다.
- 파일확장자는 URI에 포함하지 않는다.


#### URI 권한 설계

- API에 있어서 서브 도메인은 일관성 있게 사용되야 한다.
    - API 최상위 도메인과 1차 서브 도메인 이름으로 서비스를 제공해야 한다.
- 클라이언트 개발자 포탈 서브 도메인은 일관성 있게 사용되야 한다.
    - 관습적인 서브 도메인을 사용하자 예를 들면 개발자를 위한 포럼은 서브도메인으로 developers를 사용함

### 메서드

- REST에서는 HTTP 메서드를 그대로 사용함
    - POST: 등록(Create)
    - GET: 조회(Select/Read)
    - PUT: 수정(Update)
    - DELETE: 삭제(Delete)
- CRUD 네가지 상황 외에 컨트롤러를 실행하는데 POST 메서드가 사용됨

### 참고 사이트
- [restapi](http://meetup.toast.com/posts/92)
