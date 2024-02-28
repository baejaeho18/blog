---
layout: post
title: "[Git Inst] 1. 수정된 로컬에서 git pull 받기"
category: study
tags: instruction
---

로컬 프로젝트를 수정 중인데, 팀원의 수정사항을 pull 받아야 할 경우 conflict가 발생한다.

<!--more-->
```bash
C:\Users\bjh17\Projects\CIMS>git pull cims demo 
    remote: Enumerating objects: 117, done. 
    remote: Counting objects: 100% (104/104), done. 
    remote: Compressing objects: 100% (23/23), done. 
    remote: Total 63 (delta 28), reused 61 (delta 27), pack-reused 0 
    Unpacking objects: 100% (63/63), 9.68 KiB | 21.00 KiB/s, done. 
    From https://github.com/baejaeho18/CIMS 
    * branch            demo       -> FETCH_HEAD 
    3afd58d..d1409a9  demo       -> cims/demo 
    error: Your local changes to the following files would be overwritten by merge: 
            build.gradle 
            src/main/java/com/example/demo/domain/CCTV.java 
            src/main/resources/application.properties 
            src/main/resources/templates/home.html 
    Please commit your changes or stash them before you merge. 
    Aborting 
    Updating 3afd58d..d1409a9 
```

두 가지 방법이 있다.
1. stash
```bash
git stash
git stash list
git pull cims demo
git stash apply
git stash drop
```
2. commit 후, pull
```bash
git add *
git commit -m "Committing changes before pulling"
git pull cims demo
```
그러나 위의 방법들을 conflict로 인해 pull이 아예 abort되는 것을 막기 위함이다.
```bash
git pull --force cims demo
```
와 같은 무식한 방법 외에도 세련된(?) merge 방법이 있음을 기억해보자.

![stsh-apply](/assets/img/2024-02-28/stash-apply.png)
물론, conflict는 별도로(즉, 알아서) 해결해야 한다. 😀😀😀





<!-- Links -->
