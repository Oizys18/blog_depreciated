---
layout: post
title: "Github(gitlab) 저장소 옮기기 / 저장소 이관"
author: "Oizys18"
categories: [GIT]
comments: true
tags: [CS,GIT,Github,Gitlab,Basic]
---
## 목차
* TOC
{:toc}
* * *

### git repository mirroring

- gitlab 에서 github 으로 **커밋로그 포함, 그대로** 옮길 때 사용했다. 


- [최솔지](https://github.com/soulgchoi)님의 은혜..

### 저장소 옮기기

1. 원본 저장소를 복사한다.

```bash
$ git clone --mirror [원본 저장소 경로] <또는 이름>
```

2. 클론한 디렉토리 안으로 이동

```bash
$ cd [원본 저장소 이름].git
```

클론할 때 이름을 설정했으면 이름으로

3-1. 이동할 원격 저장소 경로 지정

```bash
$ git remote set-url --push origin [이동할 원격 저장소]
```

이렇게 했을 경우,

새 원격 저장소로 push

```bash
$ git push --mirror
```

3-2. 바로 원격 저장소에 push

```bash
$ git push --mirror [이동할 원격 저장소]
```


