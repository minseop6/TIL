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
- git init : 새로운 저장소 초기화
- git clone <저장소 url> : 저장소 복제
- git remote add <원격 저장소> <저장소 url> : 새로운 원격 저장소 추가

#### 기본적인 명령어
- git add <파일> : 새로운 파일 추가 또는 존재하는 파일 스테이징
- git commit -m "<메시지>" : 파일 커밋
- git push <원격 저장소> <지역 브랜치> : 지역 브랜치를 동일한 이름의 원격 브랜치에 푸싱
- git pull : origin 저장소에서 변경 사항을 가져와 현재 브랜치에 합치기
- git merge <브랜치> : 다른 브랜치를 현재 브랜치로 합치기

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
