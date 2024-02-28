---
layout: post
title: "[Git Inst] 1. 수정된 로컬에서 git pull 받기"
category: study
tags: instruction
---

로컬 프로젝트를 수정 중인데, 팀원의 수정사항을 pull 받아야 할 경우 conflict가 발생한다.

<!--more-->

>   C:\Users\bjh17\Projects\CIMS>git pull cims demo
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






<!-- Links -->
