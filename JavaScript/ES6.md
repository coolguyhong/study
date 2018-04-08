## ES6 주요 문법

### var, let, const

- 전역 변수
    + var
- 지역 변수
    + 중괄호 안에만 스코프가 있어야하는 경우에 해당
    + 수정이 가능한 변수는 let
    + 수정이 불가능한 변수는 const

### arrow 함수
- (param) => {코드}
    + function(param) {코드}
    + function 키워드를 사용하지 않고, 대신에 화살표(=>)를 사용
- 무명/익명(anonymous)함수이며 함수를 호출하려면 변수를 할당해야 함
    + let fn = (param) => {코드}
- 예시
    + es5
```javascript
var es5 = function(one, two) {
    return one + two;
}
var sum = es5(1, 2);
console.log(sum); // 3
```
    + es6
```javascript
let es6 = (one = 1, two) => {//es6 부터 parameter에 default값을 줄 수 있음
    return one + two;
}
let result = es6(2);
console.log(result) // 3
```
- arrow 표기법을 사용하는 경우 es5와 this의 의미가 다르다
    + arrow함수 자체에 this가 없으며 상위의 객체를 this라고 생각함
```javascript
// Lexical this
var bob = {
_name: "Bob",
_friends: [],
printFriends() {
this._friends.forEach(f =>
console.log(this._name + " knows " + f));
}
};
```
- 예시
    + es5
        - Sports 생성자 함수에서 this.count에 20을 할당하며 이때 this는 생성하는 인스턴스를 참조하므로 count 프로퍼티에 20이 설정
        - newSports.get()을 호출하면, get()함수 아래 setTimeout() 함수가 window 오브젝트 함수이므로 this가 window 오브젝트를 참조
```javascript
let Sports = function() {
    this.count = 20
};
Sports.prototype = {
plus: function() {
    this.count += 1;
},
get: function() {
    setTimeout(function() {
        console.log(this === window); //true
        console.log(this.plus); //undefined
    }, 1000);
  }
};
let newSports = new Sports();
newSports.get();
```
+ es6
    - 화살표 함수로 작성하면 화살표 함수 블록에서 this가 newSports 인스턴스를 참조(상위 instance가 newSports이기 때문)
```javascript
let Sports = function() {
    this.count = 20
};
Sports.prototype = {
plus: function() {
    this.count += 1;
},
get: function() {
    setTimeout() => {
        this.plus();
        console.log(this.count); //undefined
    }, 1000);
  }
};
let newSports = new Sports();
newSports.get();
```

### Promises
- 비동기 처리 방법을 제공하는 Promises 객체
```javascript
function create() {
return new Promise(function(resolve, reject){//pending상태
console.log('1: resolve');
});
};
create().then(function() {//settled상태
    console.log('3:성공');//fulfill
}, function() {
    console.log('3:실패');//reject
});
console.log('2:끝');
```
- pending
    + Promise 객체 생성하고, 나중에 호출 환경을 설정
- settled
    + pending상태가 종료되면 자동으로 상태 변환
    + 성공시 fulfill, 실패시 reject
- [Promise 설명](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Control_flow_and_error_handling#Promises)

### Destructuring
- allows binding using pattern matching, with support for matching arrays and objects
- array Destructuring
```javascript
let one, two, three, four, five;
const values = [1, 2, 3];
[one, two, three] = values;
[one, two] = values;
[one, two, three, four] = values;
[one, tow, [three, four]] = [1, 2. [73, 74]];
let one, two, three, four, other;
[one, ...other] = [1, 2, 3, 4];
```
- object Destructuring
```javascript
let {one, two} = {one: 1, nine: 9};
console.log(one, two); //1, undefined
let three, four;
({three, four} = {three: 3, four: 4});
console.log(three, four); //3, 4
//사전에 선언된 변수를 사용하려면, 소괄호 ()안에 할당 코드를 작성해야 함
```
### Operation
- 변수와 문자열 조합

```javascript
let item = 'tennis';
let sports = {
[item]: 1,
[item + 'Game']: '윔블던',
[item + 'Method']() {
return this[item];
}
}
console.log(sports.tennis); // 1
console.log(sports.tennisGame); // 윔블던
console.log(sports.tennisMethod()); // 1
```
- for of, for in 차이
```javascript
let arr = [3, 5, 7];
arr.foo = 'hello';
for (let i in arr) {
console.log(i); // logs "0", "1", "2", "foo"
}
for (let i of arr) {//리터러블 한 값만 표현이 됨(리터러블 한다는 것은 symbol)을 쓸 수 있는 것
console.log(i); // logs "3", "5", "7"
}
```

### Template String
- [Template String 설명](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Template_literals)

### Object assign()
- [Object assign 설명](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)


### ES6 참고 사이트
- [ES6 바벨 사이트 설명](https://babeljs.io/learn-es2015/#ecmascript-2015-features-destructuring)
