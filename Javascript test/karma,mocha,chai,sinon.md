# Karma, Mocha, Chai, Sinon

## Karma

- Test Runner(Environment)
- 테스트 환경을 제공하고 실행하는 역할.

## Mocha

- Test Framework(Test Lifecycle)

## Chai, Should.js

- Assertion Library in Test Suites

## Sinon

- Mocking

## TDD / BDD and Assertion Library

### TDD
![TDD](http://seokjun.kr/content/images/2016/08/tdd-work-flow.gif)

- Kent Beck에 의해 2003년에 '재발견'한 것으로 인정되는 기법.
- Red: 실패하는 테스트 코드를 작성하고
- Green: 그 테스트가 성공하도록 프로그램을 작성하고
- Refactor: 불필요한 부분을 제거(Green 상태 유지)
- 위와 같은 순서로 프로그램을 개발하는 기법이다.


### BDD

![BDD](http://arnauld.github.io/incubation/jbehave-get-started/bdd-cycle-around-tdd-cycles.png)

- Behaviour Driven Development로 주로 행위 주도 개발이라고 말하는 그것.
- Date Astels가 작성한 Article을 보통 시작점으로 삼는데, TDD와 거의 같지만 주목하는 Unit이 서로 다른 부분이 있다.
- TDD는 테스트 자체에 집중하지만 BDD는 행위(behaviour)로 대변되는 비즈니스 요구사항에 집중하는 것이다.
- [BDD 참고사이트](https://oddpoet.net/blog/2010/08/02/a-new-look-at-test-driven-development-kr/)


## Assertion Library

- 테스트 코드를 기술(describing)하기 좋게 해 주는 라이브러리.
- TDD나 BDD에 특화된 형태로 나온 것이 많다. (주목하는 단위가 다를 뿐 사실 같으니 큰 차이가 없어 보인다.)
- 다음은 [Mocha 홈페이지](https://mochajs.org/#assertions)에서 소개하는 Assertion Library이다.
    + should.js - BDD 지원
    + expect.js - BDD 지원
    + unexpected - BDD 지원
    + chai - TDD / BDD 지원

## Assert, Expect, and Should

- 테스트를 기술하는 방법의 차이
- [참고 사이트](http://chaijs.com/guide/styles/#differences)
- TDD: Assert
- BDD
    + Expect: require를 통해 가져온 expect 함수를 사용하면 된다. 모든 브라우저에서 지원하는 방법이다.
    ```javascript
    var expect = require('chai').expect
      , foo = 'bar'
      , beverages = { tea: [ 'chai', 'matcha', 'oolong' ] };

    expect(foo).to.be.a('string');
    expect(foo).to.equal('bar');
    expect(foo).to.have.lengthOf(3);
    expect(beverages).to.have.property('tea').with.lengthOf(3);
    ```
    + Should: require를 통해 should 함수를 가져온 뒤 '실행' 후 사용하면 된다. Object.prototype를 상속해서 구현된다. Internet Explorer를 제외한 최신 브라우저에서 지원된다.
    ```javascript
    var should = require('chai').should() //actually call the function
    , foo = 'bar'
    , beverages = { tea: [ 'chai', 'matcha', 'oolong' ] };

    foo.should.be.a('string');
    foo.should.equal('bar');
    foo.should.have.lengthOf(3);
    beverages.should.have.property('tea').with.lengthOf(3);
    ```

## Mocking

- 테스트 코드 작성 중에는 Mocking이 필요한 경우가 있음
- JavsScript 기반의 Mocking Library로는 [sinon.js](http://sinonjs.org/)가 대표적
- JavsScript Object나 Function, Server와 HTTP Response를 Mocking하기 위한 기능들이 제공
