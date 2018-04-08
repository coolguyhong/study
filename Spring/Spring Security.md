## Spring Security

### 인증 방식

- Spring Security 가 제공하는 인증 방식은 크리덴셜(Credential) 인증

### 인증 Flow

- Servlet Filter를 이용해 클라이언트의 요청을 가로채 리소스 제공 전 인증을 실행
- 서블릿 필터들(javax.servlet.Filter 인터페이스를 구현한 클래스들)은 기능에 따라 웹 요청을 가로챈 후 전처리 또는 후처리를 수행하거나 요청 전체를 리다이렉트하는 용도로 사용 주로 위임과 서블릿 필터을 활용해 기능을 제공

![인증Flow](https://media-api.atlassian.io/file/9774af95-2d08-4669-91ee-080a4b640a88/image?mode=full-fit&client=ac9cd94a-a769-4dac-b7f3-e1982c424403&token=eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJhYzljZDk0YS1hNzY5LTRkYWMtYjdmMy1lMTk4MmM0MjQ0MDMiLCJhY2Nlc3MiOnsidXJuOmZpbGVzdG9yZTpmaWxlOjk3NzRhZjk1LTJkMDgtNDY2OS05MWVlLTA4MGE0YjY0MGE4OCI6WyJyZWFkIl19LCJleHAiOjE1MDA3NzM5ODgsIm5iZiI6MTUwMDc3MDYyOH0.rSwDJ8xwOK_mrr5G58tLyBBXDyk3CzyzUe0QXs2wI8I)

### 참고 사이트

- [Spring Security 개념](http://tmondev.blog.me/220310743818)
