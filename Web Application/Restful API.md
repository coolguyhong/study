## Restful API

- Restful 하다는 것의 개념을 한다.
- API의 개념을 명확하게 이해한다.


### REST란 무엇인가?

- REST는 Representational state transfer의 약자로, 월드와이드웹과 같은 분산 하이퍼미디어 시스템에서 운영되는 소프트웨어 아키텍처스타일
- HTTP 프로토콜을 정확히 의도에 맞게 활용하여 디자인하게 유도 → 디자인 기준이 명확해지며, 중간계층의 컴포넌트들이 서비스를 최적화하는데 도움
- REST의 기본 원칙을 지킨 서비스 디자인을 'RESTful 하다.'라고 흔히 표현
- 잘 디자인된 API는 서비스가 여러 플랫폼을 지원하거나 공개되어야 할 때, 설명을 간결하게 해주며, 여러 문제를 쉽게 해결해 줌
- REST는 자원 지향 구조(Resource Oriented Architecture)로 웹 사이트의 이미지, 텍스트, DB 내용 등의 모든 자원에 고유한 URI를 부여합니다.
- ROA(Resource Oriented Architecture) 설계의 중심에 Resource가 있고 HTTP Method를 통해 Resource를 처리하도록 설계된 아키텍쳐를 의미


### REST 중심 규칙

- URI는 정보의 자원을 표현해야 한다.
- 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE 등)으로 표현한다.

### Controller?

- 어떤 특정 행위에 요청을 했을 때, 동사를 써서 URI 디자인 하는 것은 옳지 않음
    + 컨트롤러 리소스 정의를 통해 문제를 해결 할 수 있음
    + URI 경로의 제일 마지막 부분에 동사의 형태로 표시되어 해당 URI 접근 했을 시 행위를 생성
    + 예시: 리소스 morgan을 등록 - http://api.college.restapi.org/students/morgan/register


### RESTful한 아키텍쳐 구성 요건

- Client + Server 구조의 가장 간단한 인터페이스로 구현
    + 서버는 자원을 제공하고 클라이언트는 자원을 소비하는 구조
- Stateless
    + 세션 등으로 크라이언트와 서버의 상호작용에 따라 같은 요청이 다른 동작을 해서는 안됨
    + 똑같은 요청에 똑같은 자원을 반환
- URI를 바탕으로 이해하기 쉬운 디렉토리형 구조로 노출
    + URI만 보고 어떤 자원인지 알 수 있어야 함
- 자원의 표현은 JSON이나 XML로 표현

### RESTful PUT vs POST

- idempotent(멱등성)
    + 몇 번이고 같은 연산을 반복해도 같은 값이 나오는 것

- REST API시 PUT과 POST 사용시 고려해야 할 점
    + 명확한 URI를 갖고 있는가 여부? - 서버가 정할경우 POST 그렇지 않을 경우 PUT
    + PUT은 멱등성을 갖은 메소드

- PUT을 사용할 때
    + when you can update a resource completely through a specific resource. For instance, if you know that an article resides at http://example.org/article/1234, you can PUT a new resource representation of this article directly through a PUT on this URL.

- POST를 사용할 때
    + If you do not know the actual resource location, for instance, when you add a new article, but do not have any idea where to store it, you can POST it to an URL, and let the server decide the actual URL.


### URI(Uniform Resource Identifier)

- 균등한 리소스 식별자
- 인터넷의 어떠한 리소스를 식별하기 위해서 만들어진 것
- URI는 3부분으로 나뉘어짐: host, port, path


### URI vs URL(Uniform Resource Locator)

- [언제나 헷갈리는 URL과 URI](http://sunychoi.github.io/java/2015/04/27/uri-url.html)


### API(Application Programming Interface)란?

- 응용 프로그램에서 사용할 수 있도록, 운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스를 뜻한다. 주로 파일 제어, 창 제어, 화상 처리, 문자 제어 등을 위한 인터페이스를 제공
- 웹 API는 웹 애플리케이션 개발에서 다른 서비스에 요청을 보내고 응답을 받기 위해 정의된 명세를 일컫는다.
    + 단순히 데이터만 주고 받는 것으로 API가 정의
- 자동차의 내부적인 동작 원리는 알기 어렵지만, 액셀을 밟으면 차가 나가고, 브레이크를 밟으면 차가 멈춤. 이때, 액셀과 브레이크 등이 자동차의 API임
    + putOnAccelerator (int pushLevel): 엑셀러레이터를 발로 밟는 정도(pushLevel)를 보내면, 그만큼 차가 추진력을 받을 것이다.
    + putOnBreak (int pushLevel): 브레이크를 밟는 정도(pushLevel)를 보내면, 그만큼 차의 속력이 감소할 것이다.
    + rotateSteeringWheel (float angle): 핸들의 회전 각(angle)을 보내면 차가 그만큼 왼쪽이나 오른쪽으로 돈다.
    + changeGear (int newGear): 새로운 기어 값(newGear)을 보내면 그에 따라 차가 변속한다.
    + getCurrentSpeed(): 현재 차의 속도를 알려준다.
- 자동차의 API란 사용자가 차를 움직이게 하기 위해서, 또는 차의 상태를 알아내기 위해서는 어떻게 해야 하는지를 일정한 규칙으로 정해둔 것이다. 사용자는 차의 내부 원리에 대해 모두 알 필요 없이 자동차의 API만 익히면 차를 운전할 수 있다.
- 페이스북 API, 트위터 API도 비슷한 개념이다. 페이스북 API를 익히면 페이스북에서 정보를 얻어오고, 친구들의 사진을 다운로드하고, 페이스북에 업데이트하는 프로그램을 만들 수 있다. 예를 들어 페이스북의 그래프 API 중에 이런 것이 있다.



### 참고 사이트

- [REST API 제대로 알고 사용하기](http://meetup.toast.com/posts/92)
- [API로 무엇을 할 수 있을까?](https://talk.godo.co.kr/view.php?cate=success&mode=success2&sno=767)
- [API란?](https://sungmooncho.com/tag/api/)
- [When should we use PUT and when should we use POST?](http://restcookbook.com/HTTP%20Methods/put-vs-post/)
