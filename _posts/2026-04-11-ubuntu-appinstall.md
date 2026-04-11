---
layout: post
title: Ubuntu 앱 설치 방법 (Obsidian, VSCode)
date: 2026-04-11 17:30 +0900
categories: [Basics]
tags: [ubuntu, app, application, install, obsidian, vscode, visualstudiocode]
description: 우분투에서 Obsidian 설치 방법 설명 및 여러 설치 방법 비교
---

## 개요

vscode를 설치하는데 Ubuntu App Center에서 설치한 건 한/영 키가 안 먹는데, vscode 공홈에서 설치한 건 한/영 키가 잘 먹더라.
tar.gz 설치방식과 .deb 설치방식이 항상 둘 다 있던데 tar.gz로 설치하면 터미널에서 바로 'obsidian' 처럼 명령어를 쓸 수 없었다.
뭐가 다른걸까..


## ㄴㅇㄹ

#### Ubuntu aliasing

- alias: 긴 명령어를 짧은 별명으로 바꾸는 기능.
- 예를들어, `alias obsidian="~/Downloads/Obsidian-1.12.7.AppImage --no-sandbox"` 라고 한번 해 두면 `obsidian`만 쳐도 위 코드가 다 실행됨.
- 위 처럼 하면 일회성. Ubuntu 재부팅하면 적용 안 되어있음
-> 
```
echo 'alias obsidian="~/Downloads/Obsidian-1.12.7.AppImage --no-sandbox"' >> ~/.bashrc
source ~/.bashrc
```
하면 bashrc에 써져서 재부팅해도 기억됨.

#### echo, >>, source, bashrc

- echo: 문자열 출력하는 명령어
- `>>`(redirection): 파일을 open해서 문자열 append
- ~/.bashrc: bash가 interactive non-login shell 시작 시 실행하는 스크립트.
    - bash는 실행 모드에 따라 읽는 파일이 다름
