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

## 2020년 1월 부터 2020년 6월 30일까지 소스 수정내역(commit) 리스트 확인
`git log --oneline --after=2020-01-01 --before=2020-06-30`

## 2020년 1월 부터 2020년 6월 30일까지 mnist 폴더 소스 수정내역(commit) 리스트 확인
`git log --oneline --after=2020-01-01 --before=2020-06-30 --mnist`

## 2020년 6월 한달간 소스 수정내역(commit) 개수
`git log --oneline --after=2020-06-01 --before=2020-06-30 | wc -l`

## 소스파일 수정내역(commit) 옛날 것부터 살펴보기
`git log --reverse`

## 소스파일 수정내역(commit) 최신 것부터 3개 살펴보기
`git log --oneline -3`

## 소스파일 수정내역(commit) 옛날 것부터 3개 살펴보기

> 흔히하는 실수!
>
> `git log --oneline --reverse -3`
> 
> `-3` 먼저 적용이 되기 때문에 위 코드는 그냥 최신 커밋 3개를 reverse한 값을 프린트한다.

따라서, `git log --oneline --reverse | head -3` 라고 입력해야한다.