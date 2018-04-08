## Selenium & Nightwatch

### Selenium 1.0

- 테스트 자동화를 지원하는 다양한 소프트웨어 Tool 세트
- ThoughtWork 에서 2004년에 시작
- 초기에는 Javascript Library로 개발되었고 결국 Selenium Core로 진행
- javascript function 을 inject하여 테스트를 동작시킴

### WebDriver

- 구글에서 WebDriver라는 프로젝트로시작
- Selenium에서 사용되는 Javascript Inject방식보다, 브라우저에서 직접 제공하는 Native 지원을 원했음

### Selenium 2.0

#### Selenium 2.0 (Selenium WebDriver)

- Selenium 1.0 + WebDriver
- 브라우저를 직접적으로 조작할 수 있는 드라이버(여러 언어로 라이브러리 지원)
- 2.0 에서는 WebDriver와 통합되어, 브라우저에서 내장되어 지원하는 기능을 사용하여 브라우저를 동작시킴
- 각각의 브라우저 조작을 위한 특정 브라우저 Driver가 필요(ChromeDriver, FirefoxDriver...)

#### Selenium Grid

- 다양한 Browser, OS 및 Machine 에서의 테스트를 지원
- 병렬테스트 지원
- 중앙 집중형 관리 포인트 제공

#### Selenium IDE

- Firefox Extension 형태로 제공
- Record 및 Playback 지원
- IDs, names or XPath 등의 형태로 사용가능
![IDE](http://www.seleniumhq.org/projects/ide/selenium-ide.gif)


### Nightwatch

- Node.js 로 작성되어 있고 Selenium 2.0 을 사용하여, 웹을 위한 테스트 자동화 프레임워크
![nightwatch](http://nightwatchjs.org/img/operation.png)

#### Test Hook

- before, after, beforeEach, afterEach
- 비동기 Hook 이 필요한 경우 done을 호출하는 것으로 처리할 수 있다.
```javascript
module.exports = {
    beforeEach: function(browser, done) {
      // performing an async operation
      setTimeout(function() {
        // finished async duties
        done();
      }, 100);
    },

    after : function(browser) {
      console.log('Closing down...');
    },

    beforeEach : function(browser) {

    },

    afterEach : function () {

    },

    'step one' : function (browser) {
      browser
       // ...
    },

    'step two' : function (browser) {
      browser
      // ...
        .end();
    }
};
```

#### Nightwatch API

- Expect
    + DD style의 인터페이스
    + Chai Expect assertion library 사용
    + Language Chains 과 assertion 들이 존재함
    + expect 는 to, be 등의 chainable getters 와 equal, contain enabled 와 같은 Assertion 들로 이루어 진다.
    ```javascript
    this.demoTest = function (browser) {
        browser.expect.element('#main').text.to.not.equal('The Night Watch');

        browser.expect.element('#main').text.to.not.contain('The Night Watch');

        browser.expect.element('#main').to.have.css('display').which.does.not.equal('block');
    };
    ```
- Assert
    + 전형적인 TDD style 방식의 nightwatch에서 제공하는 assertion
    + assert : assertion이 실패했을 때, 나머지 assertion을 무시하고 테스트를 끝내버림
    + verify :  assertion이 실패했을 때, 해당 실패에 대한 로그를 남기고 테스트 계속 진행
    ```javascript
    this.demoTest = function (browser) {
        browser.assert.attributeContains('#someElement', 'href', 'google.com');
    };
    ```
- Commands
    + 웹 페이지에서 다양한 작업을 수행하기 위한 편리한 방법을 제공
    + 대개가 두개 이상의 WebDriver 프로토콜 액션을 묶어놓은 동작을 한다.
    + 각 커맨드는 마지막 인자로 콜백 함수를 받는다.
    + 커맨드 동작이 완전히 종료된 후에 콜백함수가 호출되며, main instance(browser) 와 response 가 인자로 전달된다.
    ```javascript
    this.demoTest = function (browser) {
        browser.click("#main ul li a.first", function(response) {
          this.assert.ok(browser === this, "Check if the context is right.");
          this.assert.ok(typeof response == "object", "We got a response object.");
        });
    };
    ```
- WebDriver Protocol
    + 이 명령의 대부분은 Selenium api에 대한 간단한 매핑을 제공하는 하는 기능이다.
    ```javascript
    module.exports = {
       'demo Test' : function(browser) {
          browser.url(function(result) {
            // return the current url
            console.log(result);
          });
          //
          // navigate to new url:
          browser.url('{URL}');
          //
          //
          // navigate to new url:
          browser.url('{URL}', function(result) {
            console.log(result);
          });
        }
    };
    ```
