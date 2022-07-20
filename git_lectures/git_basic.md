# 오픈소스 참여를 위한 Git/GitHub 기본실습

[강의자료](https://docs.google.com/presentation/d/1a01PRIkVKNboEVZykPXjibh4-yxoJXkvV1j04iUbd28/edit#slide=id.g8c40801e4e_0_0)

[구름 IDE를 통해서 컨테이너 생성 => 리눅스 환경을 위해](https://ide.goorm.io/my/dashboard)

## GUI vs CLI

GUI: 
- 사용자 친화적, 편하게 사용 가능
- 세부적인 기능을 사용하기 힘들다
- 협업 문제를 해결하기 어렵다

CLI:
- 세부적인 기능을 사용할 수 있다
- 문제해결 하기에 좋다 (세부기능 활용이 유연하기 때문에)
- 자동화 하기에 좋다 (스크립트)

## 기본 명령어

- `cd`: Change Directory 
    - 현재 폴더 경로 이동
- `ls`: To List Files 
    - 폴더 안에 있는 내용 확인
- `pwd`: Print Working Directory 
    - 현재 폴더 경로 확인
- `mv`: Move 
    - 파일명 변경(또는 파일경로 이동)
- `touch`: Touch 
    - 빈 파일 만들기

## Fork & Clone

`git clone ${Fork directory github https adress}`

## Git project Reading Skill

(1) 오픈소스 프로젝트 복사(fork) => "나의 작업이 올라 갈 곳"

(2) clone 소스 코드를 다운 + .git(히스토리 창고) 함께 다운

(3) 프로젝트 개발 경향을 해석
- "이 소스파일은 누가 제일 많이 개발해요?"
- "이 프로젝트는 몇 번 수정작업(commit 개수)이 이루어졌을까?"
- "이 소스파일은 최근(6개월)에 몇 번 수정되었나요?"

(4) 테스트, 실행 => 슈퍼유저(코드부터 본다? X => 직접 많이 써보기)

(5) 소스 수정 => 수정이력 저장 => add / commit

(6) 수정이력 commit => fork한 저장소에 업로드 => push

(7) Pull-Request 기능을 통해서 참여하려는 프로젝트에 수정작업 제출

## [누가 제일 많이 개발할까?](https://docs.google.com/presentation/d/1a01PRIkVKNboEVZykPXjibh4-yxoJXkvV1j04iUbd28/edit#slide=id.g8c40801e4e_0_631)

- `git log --oneline`
    - 전체 소스파일 수정내역(commit) 리스트
    - `q` 키를 눌러서 나가기
- `git log --oneline --no-merges`
    - 병합커밋(merge commit)을 제외한 실제로 소스가 수정이 된 수정내역 리스트
- `git log --oneline | wc -l`
    - 전체 소스파일 수정내역(commit) 개수 세기
    - `wc -l` 명령은 (파일) 라인 수 개수 측정
- `git shortlog -sn | nl`
    - 이 프로젝트는 누가 가장 많이 개발했나요?
    - `nl` 명령은 파일의 line number 명시(순위표시용)
- `git shortlog -sn --mnist | nl`
    - mnist 폴더를 누가 가장 많이 개발했나요?
- `git shortlog --after=2018-01-01 -sn --mnist | nl`
    - mnist 폴더를 최근에 누가 가장 많이 개발했나요?

## 오픈소스 프로젝트를 파악하는 요령

(1) 인기도, 소프트웨어 가치 => star 개수 => 좋아요 개수
- 단순히 인기있는 free software일 수 있다

(2) 협업, 활성화 정도 => commit 개수, contributor 인원수
- 오픈소스 프로젝트 본질 => "협업, 리뷰, 토론" 
- Github Insights에서 통계확인 가능

(3) 수정 내역들을 한줄씩 요약해서 보자

### 커밋 메세지 

구체적인 단어를 사용하는 것을 지향하고 Update 사용은 자제하기

- Fix: 잘못된 것을 고친 것
- Improve: 원래 잘되던 것을 개선한 것 (ex. 10초 걸리던 것을 5초로 개선)
- Add: 없던 기능, 옵션을 추가할 때
- Support: 윈도우 -> 리눅스, x86 -> ARM (환경지원)
- Refactor: 코드를 재배치
- Remove: 필요없는 것을 제거했다

## 소스파일 수정내역(commit)의 ID를 통해 내용 확인

`git log --one line` 명령어를 통해 수정내역 ID 확인 후, 

`git show ${수정내역 ID}` => `q`를 통해 나가기

- Author 저자가 누군지?
- 언제 수정한 건지?
- 왜 수정했는 지(message 확인)?
- 몇 개의 파일을 수정한건지? `diff`표시를 통해 확인가능

## [Merge commit이란?](https://docs.google.com/presentation/d/1a01PRIkVKNboEVZykPXjibh4-yxoJXkvV1j04iUbd28/edit#slide=id.g8666479880_0_1161)

Merge commit은 수정내역이 없음. 

## 전체 소스파일 수정내역(commit) 자세히 보기
`git log -p` => 수정내역을 더 세부적으로 확인가능

## 특정 소스파일기준 수정내역(commit) 리스트
- `cd /workspace/pytorch/examples/`
    - 오픈소스 작업 폴더로 이동
- `git log --oneline -- mnist/` 
    - 특정 폴더를 기준으로 소스 수정내역(commit) 리스트 확인하기 

## 특정 날짜의 소스파일 수정내역(commit) 리스트

- 2020년 1월 부터 2020년 6월 30일까지 소스 수정내역(commit) 리스트 확인
    - `git log --oneline --after=2020-01-01 --before=2020-06-30`
-  2020년 1월 부터 2020년 6월 30일까지 mnist 폴더 소스 수정내역(commit) 리스트 확인
    - `git log --oneline --after=2020-01-01 --before=2020-06-30 --mnist`
- 2020년 6월 한달간 소스 수정내역(commit) 개수
    - `git log --oneline --after=2020-06-01 --before=2020-06-30 | wc -l`
- 소스파일 수정내역(commit) 옛날 것부터 살펴보기
    - `git log --reverse`
- 소스파일 수정내역(commit) 최신 것부터 3개 살펴보기
    - `git log --oneline -3`
- 소스파일 수정내역(commit) 옛날 것부터 3개 살펴보기
    > 흔히하는 실수!
    > `git log --oneline --reverse -3`
    > 
    > `-3` 먼저 적용이 되기 때문에 위 코드는 그냥 최신 커밋 3개를 reverse한 값을 프린트한다.
    - 따라서, `git log --oneline --reverse | head -3` 라고 입력해야한다.

## Git Config

### GitHub ID/PW 캐싱데이터 삭제 (삭제시 문제없음)
다른(사람) GitHub 계정과의 충돌방지

`git config --global --unset credential.helper`

`git config --system --unset credential.helper`

### GitHub 계정 이메일 주소 및 본인영문이름
차후 소스코드 파일수정 내역(commit) 저자(author)정보  

`git config --global user.email "본인메일적으세요"`

`git config --global user.name "본인이름적으세요"`

### Git 설정내용 확인하기
`git config --list`

## Git branch & commit

### Branch 생성
작업내용을 대표하는 키워드로 Branch 명 생성추천

`git checkout -b fix-mnist`

### Branch 이동
`git checkout fix-mnist`

### Branch 삭제
`git branch -D fix-mnist`

### 브랜치를 굳이 왜 사용할까?
1. 원본을 유지하기 위해서
2. 압축파일을 따로 저장 안해도 된다
3. 다른 폴더로 복사해서 작업 안해도 된다

### 브랜치 명칭은 무엇으로 하는게 좋을까?
"내가 작업할려고 하는 내용의 요약단어"

브랜치 운영방법 => git flow => 관리자 입장

프로젝트 관리자 vs 프로젝트 참여자

### 현재 소스파일 상태(status) 확인하기
`git status`

### 소스 파일 수정한 내용 확인하기
`git diff`

### 내가 작성한 commit 확인하기
`git show`

### Add / Added / Adding?

프로젝트 디렉토리 => `CONTIBUTING.md` => 협업 규칙

보통은 현재동사를 사용

### 오픈소스 프로젝트 개발 참여

1. Fork 내가 참여할려는 오픈소스 프로젝트 복사
2. Clone 소스코드 다운 + 히스토리 내역(.git)
3. 프로젝트 개발 경향 파악(히스토리 역추적, 분석, 통계)
4. git 설정
5. 소스 수정 => ex) Commit 두개 생성
6. 내가 만든 작업을 fork 프로젝트 업로드 (push)
7. PR 내가 만든작업 commit => 오픈소스 프로젝트에 제출

### git push 할 때 필요한 토큰 생성하기

1. 접속하기 https://github.com/settings/tokens
2. Generate new token 버튼 클릭
3. 토큰 이름 정하기 ex) "test2"
4. workflow 체크
5. Generate token 토큰 생성 => 복사 => push할 때 사용
    
    (Username 에다가 token 붙혀넣기, PW는 스킵)

![Screen Shot 2022-07-19 at 4 15 35 PM](https://user-images.githubusercontent.com/67526014/179689898-88d7c42d-e3f9-45ed-b02c-59b9b088f4fe.png)

비밀번호는 안쳐도 됨.

### Clone을 잘못하여 Fork한 리파지토리로 URL 변경

`git remote remove origin`

`git remote add origin "fork 프로젝트 URL"`

### PR 보내기

1. fork한 프로젝트 GitHub 접속
2. branch => fix-mnist 변경
3. Contibute 버튼 클릭
4. Open Pull Request 버튼 클릭
5. Create Pull Request 버튼 클릭

![Screen Shot 2022-07-19 at 4 22 51 PM](https://user-images.githubusercontent.com/67526014/179691165-a33ebf5f-e4cf-4e02-b012-bfc98066c788.png)

## Rebase가 필요한 상황

git rebase 명령어 !== Rebase 개념

1. 팀프로젝트 URL 등록 
    - `git remote add upstream "오픈소스 프로젝트 URL"`
2. 최신 히스토리를 가져온다 => 내부 브랜치 자동생성("upstream/master")
    - `git fetch upstream master`
3. 베이스를 최신화 시킨다 
    - `git rebase upstream/master`
4. 강제로 fork한 프로젝트를 갱신
    - `git push origin fix-mnist --force`

        - force 푸시 안좋지 않나요? 관리자 입장에서만 ㅇㅇ 
        - 팀프로젝트를 강제로 수정하지 말라는 말! 다같이 작업하는 곳에서 force 명령어를 사용하면 위험함
        - fork한 프로젝트는 강제로 수정하는 경우가 매우 많음

![Screen Shot 2022-07-19 at 4 42 40 PM](https://user-images.githubusercontent.com/67526014/179695003-615adc63-3ccf-4e98-8b01-87d982754eaa.png)

upstream 추가 

upstream과 origin은 다르다

- upstream: 오픈소스 프로젝트 URL
- origin: fork해서 만든 프로젝트 URL

---

Q. push할 때마다 pull 받아서 충돌처리하면 안되나요?

A. git pull = fetch + merge 

Git rebase eliminates the unnecessary merge commits required by git merge

---

Q. 리베이스를 안하고 PR 머지해도 될 수 있다? 

A. Yes, but 다시 새로운 작업이 이어질 때는 작업이 꼬일 수 있음

---

## 소스코드 파일 다루기 - 기본실습

- `git status`
    - 수정한 파일 확인하기
- `git stash`
    - 수정한 내용 잠시 저장(stash) 하기
- `git status`
    - 현재 소스폴더 상태 확인하기: 아무 수정분 없음을 확인
- `git stash pop`
    - 잠시 저장(stash)해둔 내용 복구
- `git status`
    - 복구된 수정한 파일 확인하기
---

Q. git stash가 언제 필요할까?

A. before / after 테스트가 가능함

---
- `git checkout -- mnist/main.py` 
    - checkout 파일 복구 => 브랜치가 변경되지는 않음
---

Q. stash 와 checkout 파일복구의 공통점은?

A. 결과적으로 원상복구를 시킬 수 있다

---

Q. checkout 명령어의 본연의 의미?

A. ex) 도서관에서 책을 대출 받을 때 => .git 히스토리 창고에서 파일을 가져온다

---
- `git reset`
    - `git add` 한 change가 reset됨
- `git log --oneline -3`
    - 최근 커밋 3개 리스트
- `git reset --hard HEAD~1`
    - 가장 최근의 커밋 한 개 삭제
- `git commit -sm "Add import requests"`
    - `-s`옵션 포함시 라이센스 서명을 의미하는 Signed-off-by 내용을 commit message에 포함하게 된다
- `git show`
    - commit message 안에 Singed-off-by 확인
---

Q. Author 정보가 있는데 굳이? 메세지에 왜 넣는거야?

A. 라이선스 동의 => 서명 절차

CLA 절차를 밟으면 Singed-off-by가 필요없음

- https://github.com/tensorflow/tensorflow/labels?q=cla
- 구글 tensorflow 프로젝트에 PR 전송
- 라이선스 동의 절차를 안했을 때 => CLA no 라벨이 붙음

`git config --list` 를 통해서 확인해보기

---

### commit 을 수정(amend)하는 실습

가장 최근 커밋만 수정이 가능 => rewind 기능을 사용하면 중간의 commit도 수정이 가능하다.

- `git commit --amend`
    - `git add` 이후 커밋할 때 `--amend` 명령어 입력

Q. GitHub에 있는 commit도 수정할 수 있나요? YES

A. 
1. 일단 local에서 commit을 수정(amend)하고
2. 그 다음에 GitHub 히스토리를 강제로 바꿔버린다 (force push)



