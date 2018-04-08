## Selenium

### What is Selenium?

- Selenium automates browsers
- a portable software-testing framework for web applications



## e2e Test

### definition

- 소프트웨어 테스트는 규모에 다라 유닛, 통합, 시스템, 인수 이렇게 4가지로 분류한다. e2e테스트는 시스템 테스트에 속함
- 전체 시스템이 제대로 작동하는지 확인 하기 위한 테스트로 Mock이나 Stub과 같은 테스트 더블을 사용하지 않으며 최대한 실제 시스템을 사용하는 사용자 관점에서 시뮬레이션을 함


### framework

#### 헤드리스 브라우저

- Jsdom 기반의 Zombie.js, 웹킷 엔진 기반의 Pantom.js, 겟코 엔진 기반의 Slimer.js
- 커맨드 라인 명령어로 조작할 수 있는 화면이 없는 브라우저
- 크로스 브라우징 테스트 불가

#### Selenium webdriver

- webdriver.io, cucumber.js, 프로트랙터, 나이트왓치
- 웹 브라우저를 사용하여 웹 어플리케이션을 테스트하는 오픈 소스 도구
- 원래 selenium은 자바나 파이썬 등의 언어로 스크립트를 작성하면 이를 기반으로 자바스크립트를 생성하고 해당 페이지에 삽입 후 브라우저를 조작하는 간단한 구조
    + 하지만, 보안 또는 자바스크립트의 한계로 실효성이 떨어짐 → 그래서 webdriver가 나옴
- webdriver는 브라우저의 확장 기능과 os의 기본 기능 등을 이용하여 브라우저를 조작하는 구조
- 하지만, 셀레니움 서버와 자바스크립트의 궁합이 좋지 않고, 돔을 조작 하거나 셀렉팅하는데 한계가 있어 셀레니움 웹드라이버와 노드를 바인딩하여 다양한 기능을 제공하는 여러가지 형태의 프로젝트가 생겨남 → webdriver.io, nightwatch, 앵귤러 프로젝트를 위한 프로트랙터

### nightwatch

- node 기반의 e2e test framework
- selenium webdriver를 중개하여 각종 브라우저를 조작하고 동작이 기대한 것과 일치하는지 테스트
- test runner를 포함하고 있어 독자적으로 그룹화한 테스트를 한번에 실행할 수 있음
- 지속적인 통합의 파이프라인과 합칠 수 있음


### 관련 사이트

- [selenium:테스트 자동화 프레임워크](http://ojava.tistory.com/62)
-
