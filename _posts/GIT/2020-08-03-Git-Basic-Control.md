---
layout: post
title: "GIT 명령어 모음"
author: "Oizys18"
categories: [GIT Basic Control - 깃 명령어]
comments: true
tags: [CS,GIT,Basic]
---
* TOC
{:toc}
* * *


## Basic Control : 명령어 모음

### 1.설정

#### -`init`

```bash
# git initiation, Git start
$ git init <path>
```

#### -`config`

```bash
# USER 설정을 하지 않으면 commit후 remote push해도 user가 ?로 나타나고 commit count도 변하지 않는다...

# 전역 사용자명/이메일 구성하기
$ git config --global user.name “<name>”
$ git config --global user.email “<email>”

# 저장소별 사용자명/이메일 구성
$ git config user.name “<name>”
$ git config user.email “<email>”
```

#### -`status`

```bash
# git 저장소 상태 목록 (working tree, staging area, 변경사항)
$ git status
```

### 2. 로그 확인

#### - `log`

```bash
# 모든 커밋 이력보기
$ git log

# n개의 커밋 이력 확인
$ git log -n

# 변경사항 보여주는 패치와 함께 커밋 이력 표시
$ git log -p

# 기간/시간 내의 커밋 로그만 확인
$ git log --since "< time >"

# 기간/시간 이전의 커밋 로그 확인
$ git log --before "< time >"
				   # "1 month"
				   # "5 hours"
				   # "5 days"

# 두 지점 사이의 커밋 로그 확인: 커밋명, 브랜치명 태그명 등 사용가능
$ git log <start> ... <end>

# 각 항목의 로그 한줄씩 출력
$ git log --pretty=oneline

# 로그에서 복사와 붙여 넣은 정보 보기
git log -C -C -p -1 <특정 지점>
```

#### - `diff`

```bash
# 현재 작업 트리와 인덱스의 차이점 확인
$ git diff

# 인덱스와 저장소의 차이점 확인
$ git diff --cached

# 작업트리와 저장소의 차이점 확인
$ git diff HEAD

# 두 지점 사이의 차이점 확인
$ git diff <start> end
```

#### - `blame`

```bash
# 파일 커밋정보 줄 단위로 확인
$ git blame <file>

# 파일의 줄 단위의 복사, 붙여 넣기, 이동 정보 보기
$ git blame -M <파일>

# 파일의 줄 단위의 이동과 원본 파일 정보 보기
$ git blame -C -C <파일>
```

### 3. 커밋 & 브랜치 조작

#### - `add`

```bash
# 새로운 파일 추가 / 존재하는 파일 스테이징
$ git add <file>

# 파일의 일부만 스테이징
$ git add -p [<file>[<file>[<file> ... ]]]

# Git 대화모드를 사용하여 파일 추가
$ git add -i

# 수정 및 추적되는 파일의 변경사항 스테이징
$ git add -u [<path>[<path>]]
```

#### - `commit`

```bash
# 스테이징된 파일 커밋
$ git commit -m "<message>"

# 수정 및 추적되는 모든 파일의 변경 사항 커밋
$ git commit -m "<message>" -a

# 마지막 커밋 수정
$ git commit -m "<message>" --amend

# 이전 커밋을 수정하고 커밋 메세지를 재사용하기
$ git commit -C HEAD --amend
```

#### - `checkout`

```bash
# 작업트리의 변경사항 되돌리기(이전 커밋으로 돌아가기)
$ git checkout HEAD <file> [<file>]

# 다른 브랜치로 체크아웃(이동)
$ git checkout <branch>

# 브랜치를 옮기거나 브랜치명 변경하기
$ git checkout -m <branch> <new branch>
				or
$ git checkout -M <branch> <new branch>
```

#### - `cherry-pick`

```bash
# 특정 커밋 선택하여 합치기
$ git cherry-pick <commit>

# 커밋하지 않고 선택하여 합치기
$ git cherry-pick -n <commit>
```

#### - `merge`

```bash
# 현재 브랜치에서 다른 브랜치와의 diff를 확인하고 합친다.
$ git checkout <끌어올 브랜치>
$ git merge <따라갈 브랜치>
$ git push

# 커밋하지 않고 합치기
$ git merge --no-commit <branch>

# 브랜치의 이력을 다른 브랜치에 합치기
$ git merge --squash <branch>
```

#### - `reset`

```bash
# 커밋되지 않고 스테이징된 변경사항 재설정
$ git reset HEAD <file> [<file>]
```

#### - `branch`

```bash
# 현재 branch 상황 확인
$ git branch

# 원격 브랜치 목록 보기
$ git branch -r

# 지역과 원격을 포함한 모든 브랜치 목록 보기
$ git branch -a

# 브랜치 삭제
	# 삭제할 브랜치가 현재 브랜치에 합쳐졌을 경우
	$ git branch -d <branch>

	# 삭제할 브랜치가 현재 브랜치에 합쳐지지 않았어도 삭제
	$ git branch -D <branch>

# 현재 브랜치에서 새로운 브랜치 생성
$ git branch <new branch>

# 현재 브랜치에서 새로운 브랜치 생성하고 체크아웃하기
$ git branch -b <new branch>

# 다른 시작지점에서 브랜치 생성하기
$ git branch <new branch> <location>

# 기존의 브랜치를 새로운 브랜치로 덮어쓰기
$ git branch -f <branch> [<new branch location>]
```

### 4.원격저장소

#### - `clone`

```bash
# 저장소 복제
$ git clone <repo>

# 마지막 200개의 커밋만 포함한 저장소 복제
$ git clone --depth 200
```

#### - `remote`

```bash
# 새로운 원격 저장소 추가
$ git remote add <custom repo name> <repo url>

# 원격 저장소 목록 출력
$ git remote -v

# 원격 저장소에서 쓸모가 없어진 원격 브랜치 제거하기
$ git remote prune <remote repo>

# 원격 저장소 제거, 관련 브랜치 제거
$ git remote rm <remote repo>
```

#### - `push`

```bash
# 지역 브랜치를 원격 브랜치에 푸싱하기
$ git push <remote repo> <local branch>:<remote branch>

# 지역 브랜치를 동일한 이름의 원격 브랜치에 푸싱하기
$ git push <remote repo> <local branch>

# ex) origin 브랜치를 master 브랜치로 푸싱한다.
$ git push origin master

# 특정 브랜치에 정의된 remote repository가 있다면(기본 원격 원점이 사용된다)
$ git push
```

#### - `pull`

```bash
# 원격 저장소에서 변경 사항을 가져와 현재 브랜치에 합치기
$ git pull <remote repo>

# origin 저장소에서 변경 사항을 가져와 현재 브랜치에 합치기
$ git pull
```

#### - `fetch`

```bash
# origin 저장소에서 합치지 않고 지역 브랜치로 변경 사항 가져오기
$ git fetch

# 원격 저장소에서 합치지 않고 지역 브랜치로 변경사항 가져오기
$ git fetch <remote repo>
```

#### - `rm`

```bash
기본적으로 파일 삭제 -> commit 해야함

1. Untracked 파일 삭제
- 일반적 bash 파일 삭제, rm -rf 사용

2. Tracked 파일 삭제
2-1. 로컬 디렉토리와 git 저장소에서 모두 삭제
$ git rm <filename>
$ git commit -m 'Delete reason'

2-2. 로컬에서는 삭제하지 않지만 git에서는 삭제
# (git add로 커밋하지 말아야할 파일을 커밋했을 경우)
# 이 방법 사용하면 로컬에서는 파일 유지, 저장소에서만 파일 삭제 가능
$ git rm --cached <filename>
$ git commit -m 'Delete reason'

3. 기타
# -f 변경사항을 커밋하지 않았을 경우 강제로 삭제
$ git rm -f <filename>

# -r 디렉토리 삭제
$ git rm -r <directory name>
```

