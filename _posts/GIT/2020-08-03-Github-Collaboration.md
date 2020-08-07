---
layout: post
title: "Github을 이용한 협업"
author: "Oizys18"
categories: [GIT]
comments: true
tags: [CS,GIT,Github,Basic]
---
* TOC
{:toc}
* * *



```
# 폴더 생성 후 git 시작
$ git init .

# git 환경 체크
$ ls .git

# local git configuration 확인
$ cat .git/config            #refs 폴더 속 git의 해쉬 존재

$ git status
```

- 협업 중 문제 발생시 : Issue

```
Issues에 추가 가능, 태그도 달 수 있다.
```

### Case 1

```
- 동일 파일 동시작업 X

1. 작업 시간을 나눈다    or   2. 작업 폴더(파일)을 나눈다.
```

```
git pull하기 전,
항상
$ git add ~
$ git commit -m '~'
하자

```

- 만약 다른 파일을 push 해서 conflict 생겼을 때,

```
VIM이 자동으로 open됨
- esc
$ :wq
$ git pull

Auto merge된다!
: 즉, 같은 파일을 수정하지 않으면 됨
```

- 결론 : 같은 시간대에, 같은 파일을 수정하지 말자!