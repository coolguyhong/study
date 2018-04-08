### Vue 사용자 정보 및 권한 보관 고려사항

- Client Application은 사용자정보를 Client에 보관하여 처리 해야 한다.
- Vue는 SPA 이기 때문에 로그인 세션이 만료 혹은 종료되었을 경우, 로그인 페이지로의 전환을 직접 작성해야 한다.
    + 서버사이드 페이지(JSP, PHP 등)의 경우에는 서버에 의한 Redirect 를 통해 로그인페이지로 전환 되었을 것임
- Vue 내부의 Routing이 아닌 브라우저에 의한 페이지 전환시 사용자 정보가 소실
    + 어떤 시점에 사용자정보를 로드 할 것인지에 대한 전략이 필요
    + 어떻게 사용자 정보를 저장할 것인지 고려해야 함

![Flow](https://media-api.atlassian.io/file/5233ccea-f471-4de6-9fde-a7a5c4c07ea2/image?mode=full-fit&client=ac9cd94a-a769-4dac-b7f3-e1982c424403&token=eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJhYzljZDk0YS1hNzY5LTRkYWMtYjdmMy1lMTk4MmM0MjQ0MDMiLCJhY2Nlc3MiOnsidXJuOmZpbGVzdG9yZTpmaWxlOjUyMzNjY2VhLWY0NzEtNGRlNi05ZmRlLWE3YTVjNGMwN2VhMiI6WyJyZWFkIl19LCJleHAiOjE1MDA4MTc1NTAsIm5iZiI6MTUwMDgxNDE5MH0._HCku5ckEs0BLHntyAzDlvfivSTlrXDJNQ9X2bEn7do)
