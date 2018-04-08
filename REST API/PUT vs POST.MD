## PUT vs POST

- HTTP PUT 요청과 POST 요청의 차이를 알 수 있다.

### 고려사항

- 멱등성(Idempotent)
    + 여러번 request를 해도 같은 response를 반환해주는 경우

- 리소스 결정권
    + 서버에 의해 결정되는가? vs 클라이언트에 의해 결정되는가?
    + POST의 경우에는 클라이언트가 실제 저장해야할 리소스 위치를 모르므로 서버에서 처리 하도록 함
    + PUT을 사용하면 클라이언트가 이미 변경 대상 리소스의 위치를 알고 있어서, 특정 업데이트 대상 리소스를 갱신할 수 있음

### POST

- 수행 기능은 서버에 의해 결정되고 보통 요청 URI에 의존함
    + 추가되는(posted) 엔티티는 그 URI의 하위에 붙는 것
- 리소스의 위치를 지정하지 않았을때 리소스를 생성하기 위해 사용하는 연산
- 클라이언트가 새로 생성될 리소스의 URI를 정확하게 할 필요가 없을때 사용한다. 대부분의 경우 클라이언트는 부모 또는 factory 리소스의 URI만 알면 됨
- 예를 들면 연산을 수행하면 /dogs/2 에 생기고, 그 다음번엔 /dogs/3 등 매번 다른곳에 새로운 리소스가 생성될 수 있으므로, 이 연산은 idempotent 하지 않음

```java
POST /dogs HTTP/1.1
{ "name": "blue", "age": 5 }
HTTP/1.1 201 Created
```

### PUT

- 클라이언트에서 서버에게 보내주는 정보(application state)로 새로운 리소스의 URI가 예측되고 결정됨
    + 리소스의 대표이름(아이디나 키)이 클라이언트에 의해 결정됨
- 리소스의 위치가 지정되었을때 생성 또는 업데이트를 위해 사용할 수 있음
- /dogs 의 프로퍼티가 name 과 age 뿐이라면, 이건 몇 번을 수행하더라도, 같은 결과를 보장한다. 다시 말해 idempotent 함

```java
POST /dogs/3 HTTP/1.1
{ "name": "blue", "age": 5 }
```


### 결론

- 새로운 리소스의 URI가 클라이언트에 의해 결정될 경우 PUT을 사용한다. 새로운 리소스의 URI가 서버에 의해 결정될 경우 POST를 사용한다.
- 멱등성을 갖지 않고 리소스를 서버가 결정해주면 POST, 멱등성을 가지고 있으면서 리소스를 클라이언트가 결정하면 PUT이다.

### 참고 사이트

- [put vs post](http://restcookbook.com/HTTP%20Methods/put-vs-post/)
- [REST API: PUT VS POST](https://1ambda.github.io/javascripts/rest-api-put-vs-post/)
- [The Resource-Oriented Architecture-2](http://greatkim91.tistory.com/14)
