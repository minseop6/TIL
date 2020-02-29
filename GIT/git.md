# GIT
----------
## GIT이란?
- 버전 관리 시스템(VCS, Version Control System)의 한 종류
- 여러명이 동시에 작업하는 병렬 개발이 가능
- 분산 버전관리이기 때문에 연결되지 않은 환경에서도 개발 가능

## GIT 기본 용어
- Repository : 저장소를 의미
 - 저장소는 히스토리, 태그, 소스의 가지치기 혹은 branch에 따라 버전을 저장
 - 저장소를 통해 작업자가 변경한 모든 히스토리를 확인 가능
 - 원격 저장소(Remote Repository) : 파일이 원격 저장소 전용 서버에서 관리되며 여러 사람이 함께 공유하기 위한 저장소
 - 로컬 저장소(Local Repository) : 내 PC에 파일이 저장되는 개인 전용 저장소


- Woring Tree : 저장소를 어느 한 시점을 바라보는 작업자의 현재 시점
- Staging Area : 저장소에 커밋하기 전에 커밋을 준비하는 위치
- Commit : 현재 변경된 작업 상태를 점검을 마치면 확정하고 저장소에 저장하는 작업
- Head : 현재 작업중인 Branch
- Branch : 가지 또는 분기점
- Merge : 다른 Branch의 내용을 현재 Branch로 가져와 합치는 작업


## GIT 주요 명령어

#### 설정 & 초기화
- git config --global user.name <사용자명> : 전역 사용자명 설정
- git config --global user.email <이메일> : 전역 이메일 설정
- git init : 새로운 저장소 초기화
- git clone <저장소 url> : 저장소 복제
- git remote add <원격 저장소> <저장소 url> : 새로운 원격 저장소 추가

#### 기본적인 명령어
- git add <파일> : 새로운 파일 추가 또는 존재하는 파일 스테이징
- git commit -m "<메시지>" : 파일 커밋
- git push <원격 저장소> <지역 브랜치> : 지역 브랜치를 동일한 이름의 원격 브랜치에 푸싱
- git pull : origin 저장소에서 변경 사항을 가져와 현재 브랜치에 합치기
- git merge <브랜치> : 다른 브랜치를 현재 브랜치로 합치기

#### 브랜치 관리
- git branch :  지역 브랜치 목록 보기
  - -r : 원격 브랜치 목록 보기
  - -a : 모든(지역, 원격) 브랜치 목록 보기
- git branch <새로운 브랜치> : 현재 브랜치에서 새로운 브랜치 생성
  - -b : 새로운 브랜치를 생성하면서 체크아웃
  - -m : 브랜치를 옮기거나 브랜치명 변경
- git checkout <브랜치> : 다른 브랜치로 체크아웃
- git merge <브랜치> : 다른 브랜치를 현재 브랜치로 합치기
  - --squash : 브랜치의 이력을 다른 브랜치에 합치기
- git cherry-pick <커밋명> : 하나의 커밋만 선택하여 합치기
- git branch -d <삭제할 브랜치> : 브랜치 삭제하기(삭제할 브랜치가 현재 브랜치에 합쳐졌을 경우)
- git branch -d <삭제할 브랜치> : 브랜치 삭제하기(삭제할 브랜치가 현재 브랜치에 합쳐지지 않았을 경우)

#### GIT 이력

#### 원격 저장소

## 두개의 브랜치 합치기
#### Merge
- 기본적인 브랜치 병합기능
- 합치려고 하는 대상의 브랜치의 변경사항을 타겟 브랜치에 모두 반영하여 머지 커밋을 남김

<img src="../img/GIT/git/merge.jpg" width="300" height="300">

```git
$ git checkout master
$ git merge feature
```

#### Merge squash
- `--squash` 옵션은 해당 브랜치의 커밋 전체를 통합한 커밋을 타켓 브랜치에 머지하는 옵션

<img src="../img/GIT/git/merge_squash.jpg" width="300" height="300">

```git
$ git checkout master
$ git merge --squash feature
```

#### Rebase
- 브랜치를 다른 브랜치로 합칠 수 있는 기능
- 머지와는 다르게 `dev`브랜치의 변경사항 전부를 `master`브랜치에 푸쉬하는 것과 동일

<img src="../img/GIT/git/rebase.jpg" width="300" height="300">

```git
$ git checkout feature
$ git rebase master
```

##### Merge와의 차이점
- Merge는 어느 시점에 어떤 브랜치가 머지 되었는지 커밋을 통해 알기 쉽지만 불필요한 커밋이 생성됨
- Rebase는 브랜치의 베이스를 변경하는 것으로 불필요한 머지 커밋이 남지않지만 Rebase후 브랜치의 변경사항이 반영되지 않은 사용자는 히스토리가 꼬이게됨

#### Cherry pick
- 다른 브랜치에서 어떤 하나의 커밋만 현재 브랜치로 가져오는 기능

```git
$ git checkout master
$ git cherry-pick <가져올 커밋 해쉬>
```

## 변경사항 임시 저장
#### Stash
- 현재 작업 중인 변경사항들을 잠시 스택에 저장할 수 있는 기능
- 마무리되지 않은 작업이 있을 때 다른 브랜치로 체크아웃해야하는 경우에 사용
- stash에 이름 지정 가능
- 이름을 지정하지 않을 경우 LIFO로 stash를 가져옴

```git
$ git stash # 현재 변경 사항들을 스택에 저장
$ git stash list # stash 목록을 확인
$ git stash apply # 가장 최근의 스태쉬를 다시 불러옴

$ git stash <stash 이름> # stash에 이름을 지정해서 현재 변경사항들을 스택에 저장
$ git stash apply <stash 이름> # <stash 이름>을 가진 stash를 불러옴
```

## 커밋 되돌리기
#### Reset
- 지정한 커밋의 상태로 돌아가는 기능
- reset을 사용하면 지정한 커밋 이후의 히스토리는 모두 사라짐
- 사용가능한 옵션
  - hard : 삭제된 내용들은 사라짐
  - soft : 삭제된 내용들은 스테이지로 이동
  - mixed : 삭제된 내용들은 스테이지에 올라가지 않은 상태가 됨

```git
$ git reset <옵션> <커밋명>
```

#### Revert
- 특정 커밋의 변경사항을 되돌리는 기능

```git
$ git revert <커밋명> # 특정 커밋을 되돌림
$ git revert <커밋명>..<커밋명> # 커밋의 범위를 지정하여 되돌림
$ git revert HEAD # 현재 헤드가 위치한 커밋을 되돌림
```
