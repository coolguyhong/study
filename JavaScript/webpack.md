# webpack

## Javascript 모듈 시스템과 webpack

- Javasciprt  모듈화 명세 : CommonJS, AMD(Asynchronous Module Definition)
- 모듈로 만든 파일을 바로 웹 페이지에 넣어 브라우저에 실행할 수 있는 형태로 변경이 필요함 → webpack
- webpack 은 CommonJS, AMD 두 가지 모듈화 명세를 지원
- 모듈의 스코프 : 컴파일 과정에서 각 모듈은 함수로 감싸져 지역변수가 된다. (전역변수를 피하려고 따로 함수로 감싸지 않아도 됨)
- webpack의 주요 네 가지 개념
    + 엔트리
    + 아웃풋
    + 로더
    + 플러그인

## webpack 사용방법

- webpack은 Node.js 가 설치된 환경에서 실행됨
- webpack 컴파일
    + webapck ./entry.js bundle.js
    + --watch 옵션 사용시 모듈 파일이 변경될 때마다 재컴파일
    + webpack.config.js 설정파일 사용 : webapck

    ```javascript
      module.exports = {
          context: __dirname + '/app', // 모듈 파일 폴더
          entry: { // 엔트리 파일 목록
              app: './app.js'
          },
          output: {
              path: __dirname + '/dist', // 번들 파일 폴더
              filename: '[name].bundle.js' // 번들 파일 이름 규칙
          }
      }
    ```
- 엔트리 파일이 하나인 경우
![webpack_when_entryfile_is_one](http://d2.naver.com/content/images/2016/02/webpack-1.png)
```javascript
entry: './app.js',
output: {
    path: __dirname + '/dist', // 번들 파일 폴더
    filename: 'bundle.js'
}
```
```javascript
// index.js와의 읜존성은 없지만 html에서 googleAnalytics.js가 필요 할 경우 이렇게 명시
entry: ['src/index.js', 'src/googleAnalytics.js'],
output: {
    path: __dirname + '/dist', // 번들 파일 폴더
    filename: 'bundle.js'
}
```
- 엔트리 파일이 여러 개인 경우
![webpack_when_entryfile_is_not_one](http://d2.naver.com/content/images/2016/02/webpack-2.png)
```javascript
entry: {
    indexEntry: 'src/index.js',
    profileEntry: 'src/googleAnalytics.js'
},
output: {
    path: __dirname + '/dist', // 번들 파일 폴더
    filename: '[name].bundle.js' // 번들 파일 이름 규칙
}
```

## 로더

- 자바스크립트 파일 뿐 아니라 다양한 리소스(이미지, 폰트, 스타일시트, ...)를 JavaScript에서 바로 사용할 수 있는 형태로 로딩하는 기능.
- 웹팩은 자바스크립트 밖에 모른다. 비 자바스크립트 파일을 웹팩이 이해 하게끔 변경해주는게 로더
- 로더가 설치되면  webpack.config.js 파일에 로더 관련 설정이 추가된다.
```javascript
module.exports = {
    ...
    output : {
        ...
    },
    module : {
        rules: [
        {
            test: /\.vue$/,  // 정규식을 이용해서 로더에 사용될 파일을 검출
            loader: 'vue-loader'  // 일치하는 파일에 사용되는 로더를 호출
        },
        {
            test: /\.js$/,
            exclude: /(node_modules|bower_components)/,
            use: {
                loader: 'babel-loader',
                options: {
                    presets: ['env']
                }
            }
        }]
    }
}
```

## 플러그인

- 로더가 파일단위로 처리하는 반면 플러그인은 번들된 결과물을 처리한다. (번들된 자바스크립트 난독화, 특정 텍스트 추출 등..)
- 사용 예시
    + UglifyJsPlugin: 로더로 처리된 자바스크립트 결과물을 난독화 처리하는 플러그인이다.
    ```javascript
      const webpack = require('webpack')

      module.exports = {
          plugins: [
            new webpack.optimize.UglifyJsPlugin(),
          ]
      }
    ```
    + ExtractTextPlugin: 특정 파일(css 등)을 따로 번들링 할 수 있게 해주는 플러그인
    ```javascript
      const ExtractTextPlugin = require('extract-text-webpack-plugin')

      module.exports = {
        module: {
          rules: [{
            test: /\.scss$/,
            use: ExtractTextPlugin.extract({
              fallback: 'style-loader',
              use: ['css-loader', 'sass-loader']
            })
          }]
        },
        plugins: [
          new ExtractTextPlugin('style.css')
        ]
      };
    ```

## 개발자 도구 연동

- webpack 사용 시 브라우저에서 실행되는 코드는 실제 작성된 코드가 아님 → Debugging 하는데 어려움
- webpack.config.js 파일에 소스 맵 설정을 사용하면 원래의 파일 구조를 확인할 수 있음
```javascript
module.exports = {
    ...
    devtool: '#inline-source-map'
}
```
- 브라우저에서 개발자 도구를 실행하면 webpack:// 도메인 아래에 모듈을 구성하는 파일 구조가 나타난다.
![ide_webpack](http://d2.naver.com/content/images/2016/02/webpack-5.png)

## 정리

- 웹팩은 기본적으로 모듈 번들러이다.
- 의존성 그래프에서 엔트리로 그래프의 시작점을 설정하면 웹팩은 모든 자원을 모듈로 로딩한 후 아웃풋으로 묶어준다.
- 로더로 각 모듈별로 바벨, 사스변환 등의 처리하고 이 결과를 플러그인이 받아 난독화, 텍스트 추출 등의 추가 작업을 한다.

## 참고할 만한 블로그

- [JavaScript 모듈화 도구, webpack](http://d2.naver.com/helloworld/0239818)
- [webpack 기본 개념](http://blog.jeonghwan.net/js/2017/05/15/webpack.html)
- [webpack 기본부터 배포까지](https://jaewonism.com/posts/35)
- [webpack의 혼란스런 사항들](https://github.com/FEDevelopers/tech.description/wiki/Webpack%EC%9D%98-%ED%98%BC%EB%9E%80%EC%8A%A4%EB%9F%B0-%EC%82%AC%ED%95%AD%EB%93%A4)
