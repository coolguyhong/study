## Docekr

- 컨테이너 기반의 오픈소스 가상화 플랫폼
- 컨테이너 기반 가상화 도구
- 컨테이너라는 리눅스 커널 레벨에서 제공하는 격리된 가상 공간을 사용


### 이미지(Image)와 컨테이너(Container)

- Image
    + 필요한 프로그램, 라이브러리, 소스 등을 설치한 뒤에 이를 파일로 만든 것
    + 컨테이너 실행에 필요한 파일과 설정값등을 포함하고 있는 것
- Container
    + 이미지가 실행된 상태
- 이미지를 여러 번 실행하면 여러 개의 컨테이너가 생성
- 이미지는 일종의 실행파일, 컨테이너는 프로세스와 유사한 개념


### Repository 연계

- Container Image를 중앙의 Repository에 저장했다가, 다른 환경에서 가져다가 사용할 수 있음
    + local pc에서 mysql, apache, tomcat등을 각 컨테이너에 넣어서 개발을 한 후에, 테스트 환경등으로 옮길때, Container를 repository에 저장했다가 테스트환경에서 pulling(당겨서) 똑같은 테스트환경을 꾸밀 수 있다는 것

### Base Image vs Dockerfile

- Base Image
    + 기본적인 인스톨 이미지
- Dockerfile
    + 기본적인 인스톨 이미지와 그 위에 추가로 설치되는 스크립트
    + Base Image가 Ubuntu OS 이미지라면, Docker File은 Ubuntu OS + Apache, MySQL을 인스톨하는 스크립트


### Container vs vm

- container vs vm
    ![container vs vm](https://cdn-images-1.medium.com/max/1250/1*wOBkzBpi1Hl9Nr__Jszplg.png)
- vm은 하드웨어를 가상화 하고, 그 위에 Guest OS가 올라감
- container는 docker-engine 위에 application 실행에 필요한 바이너리만 올라감. 그외 커널 부분은 호스트의 커널을 공유
