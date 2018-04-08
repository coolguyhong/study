## Nodejs

### 개념

- 2009년 Ryan Dahl에 node.js 탄생
- 구글이 만든 v8엔진을 JavaScript 엔진으로 사용
- event-driven + non-blocking IO를 결합
- server쪽에서 JavaScript를 활용할 수 있게 도와줌

### Web vs Nodejs

- RunTime 환경에서 접근해야함
    - Web 환경에서 client 구현가능, Nodejs 환경에서 server 구현
- alert('Hello world')
    - Web Broser에서 제공하는 함수이기 때문에 Nodejs에서 사용을 하게 된다면 에러가 발생
    - ex) '법원에 가서 주사를 놔주세요' 하는 꼴

### 특징 및 장점

- v8엔진을 이용하기 때문에 속도나 성능이 괜찮음
- event-driven과  non-blocking 패러다임을 이용하여 이러한 경우가 적합할 경우 엄청난 퍼포먼스 만들 수 있음
- client: JavaScript / server: JavaScript 사용하기 때문에 JavaScript로 하나의 어플리케이션을 구현할 수 있음


### package.json

- 패키지에 관한 정보와 의존중인 버전에 관한 정보를 담고 있음
- name과 version은 필수적으로 입력 되어야 함
- 의존성을 표현하는 것: dependencies, devDependencies, peerDependendependencies는 일반적인 경우 의존하고 있다는 것을 알려주는 곳cies
    - dependencies: 일반적인 경우 의존하고 있다는 것을 알려주는 곳
    - devDependencies: 개발 모드일 때만 의존하는 것,  실제로 배포할 때는 필요없는 테스트 도구나 웹팩, 바벨같은 것들을 넣어두면 됨
    - peerDependencies: 직접 require은 하지 않지만 호환되는 패키지의 목록

### npm

- the package manager for JavaScript and the world’s largest software registry
