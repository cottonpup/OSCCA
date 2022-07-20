# 오픈소스 참여를 위한 Git/GitHub 고급실습

[강의자료](https://docs.google.com/presentation/d/1wZNt_3AHDg7guPjIn1vD-CYXupGzHU_c2wWb4PSwMJg/edit#slide=id.g86633d5308_0_0)

고급 실습 환경 준비

1. 교육자료(고급)
2. 구글 git bash 검색 => 다운로드 설치
3. clone 과 config 기본 세팅 준비

## 오픈소스 프로젝트 협업개발 도중 Rebase가 필요한 상황

오픈소스 프로젝트 작업 중 다른 사업 먼저 Merge하였을 때

- git fetch upstream master => "upstream/master" 내부 브랜치 자동 생성 됨
- git rebase upstream/master 
- git rebase -i, --interactive => 되감기 기능

### 되감기(Rewind) 실습
- `git rebase -i --root`
    - root => 전체범위
    - 옛날 커밋부터 보인다
    - 감을 수 있는 커밋 후보들을 보여줌
    - pick => edit으로 변경 (breakpoint)
- `git rebase -i HEAD~10`
- `git rebase --continue`
    - 감겨진 커밋들 다시 되돌리기

### 가장 오래된 역사 부터 두번째 commit 이후에 새로운 커밋 commit 3개 넣기

`touch hello_1.c && git add hello_1.c && git commit -m 'Add hello_1.c'` 

=> And 연산자를 CLI에서도 사용가능 => 앞 명령어가 실행되지 않으면 뒤도 실행되지 않음

![Screen Shot 2022-07-20 at 12 45 27 PM](https://user-images.githubusercontent.com/67526014/179892242-a74108d6-a530-4b6f-9dea-264131c60d0c.png)

## 히스토리 초기화 방법

- `git reset --hard origin/master`
    - 내부 브랜치에 의해 히스토리 초기화 

## 위 예제에서 넣은 (중간에 낀) 3개를 commit을 1개로 합치기

되감기 동작을 통해 hello_3 + hello_2 커밋 병합하기

- `git reset --hard` 와 `git reset --soft` 의 차이점
    - 둘 다 히스토리를 삭제하는 건 같으나, `--hard` 는 완전히 파일까지 삭제하고 `--soft` 는 파일은 살려둔다.

- git rebase를 취소하는 방법:
    - `git rebase --abort`

## 가장 오래된 역사에서 두번째 커밋 "Add knapsack problem PDF" 삭제하기

- `git rebase -i --root`
- `git reset --hard HEAD~1`
- `git rebase --continue`

## git blame 실습

해당 소스라인 대해서 누가 마지막으로 수정을 했는지 commit ID 추적이 가능하다

- git reset --hard origin/main
    - 히스토리 원상복구
- git blame node_http_parser.cc
    - blame 을 통해서 Parser 클래스 소스구현 라인중에 최초 commit 을 찾아보자
- git reset --hard <commit ID>~1
    - 특정 commit 이전 역사로 되돌리기
    - ~1 => 한단계 더 과거
- git log --oneline --reverse -- src/node_http_parser.cc | head -1
    - 진짜 최초 커밋일까?
    - git show 1a126ed11c => 해보면 최초 커밋이 아님 (모두 초록색 텍스트가 아님)
    - 과거로 돌아가봤더니 src 폴더가 존재 x
    - 과거에는 src 폴더가 존재하지 않았음. src 기준으로 1a126ed11c가 최초 커밋은 맞음
- git log --oneline --reverse -- node.cc | head -1
    - 19478ed4b1 => 이게 진짜 최초 커밋!
- git log --oneline --reverse | head -3 
    - 전체 커밋 기준으로 node 프로젝트가 처음 만들어질 때 최초로부터 Commit 3개

https://github.com/nodejs/node/commit/42ee16978e81a0f1fba0768e163b5e9584178fa3

## rebase 실습

![Screen Shot 2022-07-20 at 6 19 55 PM](https://user-images.githubusercontent.com/67526014/179946454-b89659bf-c916-4506-82d2-6610a881cb1d.png)

base 충돌

> Your branch and 'origin/master' have diverged,
> and have 1 and 1 different commits each, respectively.
>  (use "git pull" to merge the remote branch into yours)

- git remote -v

fatal: 'upstream' does not appear to be a git repository

fatal: Could not read from remote repository.

Please make sure you have the correct access rights

and the repository exists.

위와 같은 에러가 뜨면 `git remote add upstream 팀프로젝트 URL` 입력

- git fetch upstream master
- git rebase upstream/master
- git push origin master --force


