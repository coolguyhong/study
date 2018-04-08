## Git

### 로컬 저장소는 git이 관리하는 세 그루의 나무로 구성
- Working directory: 실제 파일들
- Index: staging area
- HEAD: commit한 것, 마지막 커밋의 스냅샷


### 가지치기
- branch 새로 만들기
    + git checkout -b feature_x
- 기존 branch 가져오기
    + git checkout master
- branch 삭제
    + git branch -d feature_x


### merge
- fast-forward
    + 합칠 Branch가 현재 Branch와 분기된 이후, 현재 Branch에 새로 생성된 Commit이 없을 경우 현재 Branch를 가리키는 HEAD를 합칠 Branch의 마지막 Commit으로 옮김으로써 Merge를 수행하는 방법

- non fast-forward
    + fast-forward 방식이 가능하더라도 non fast-forward방식으로 병합옵션을 할 경우 bugfix 브랜치가 남게 되고 새로운 master브랜치가 됨.
    + 브랜치가 그대로 남기 때문에 실행한 작업 확인 및 브랜치 관리 면에서 더 유용할 수 있음

- merge
    + 여러 개의 브랜치를 하나로 모을 수 있음
    + 이력관리가 쉬움

- rebase
    + 이력은 단순해지지만, 원래의 커밋 이력이 변경되어 정확한 이력을 남길 수가 없음


### reset
- hard
    + 무조건 맨처음 브랜치를 따왔던 시점으로 수정사항이 남지 않음
    + 되돌리는 옵션이 없기 때문에 조심해서 사용해야 함
    + git reset --hard origin/master
- mixed
    + 가장 최근의 커밋으로 되돌림
    + staging area역시 비움
    + git reset 명령어의 default는 --mixed임
- soft
    + HEAD를 이전 커밋된 스냅샷으로 변경


### 성공적인 git branching 전략
- [깃 브랜친 전략](http://nvie.com/posts/a-successful-git-branching-model/)


### 참고 사이트
- https://backlogtool.com/git-guide/kr/stepup/stepup1_4.html
- http://mobicon.tistory.com/280
- http://dogfeet.github.io/articles/2011/a-successful-git-branching-model.html
- https://nolboo.kim/blog/2013/10/06/github-for-beginner/
- http://rogerdudler.github.io/git-guide/index.ko.html
- https://github.com/corean/git-study
