---
layout: post
title: Ubuntu 한영전환 방법
date: 2026-04-06 15:30 +0900
categories: [Basics]
tags: [ubuntu, keyboard, korean, english]
description: 우분투에서 한영전환 방법 및 그 배경
---

## 개요

Ubuntu에서 한영전환이 되긴 했는데, alt로 인식되면서 한영전환이 느리고, alt+space 등 여러 단축키로 실행될 때도 있었다. 그리고 뭔가 한국어 입력이 느린 것 같아서 이런 것들을 해결하기 위해 여러 방법을 찾아봤다.

방법은..
1. fcitx 설정
2. xmodmap 설정
이다.


## Ubuntu Input Framework

- Input Framework: 키보드로 입력한 걸 원하는 문자(한글/한자/일본어 등)으로 변환하는 시스템

1. IBus (Inteligent Input Bus): GNOME 기본 입력기
    - GNOME: Desktop Environment UI를 담당하는 시스템.
        - 창 열기/닫기/이동, 파일 탐색기, 설정, 앱 실행 화면, 인풋/아웃풋 처리 등
        - GNOME 말고도 KDE Plasma, Xfce, LXDE 등 있음
        - Ubuntu의 기본 UI가 GNOME
2. FCITX (Flexible Context-aware Input Tool with eXtension): 빠르고 커스터마이징 쉬움

느린 입력과 버튼 커스터마이징이 문제였으므로 FCITX로 설치해준다: 
```
sudo apt install fcitx5 fcitx5-hangul
```
을 입력하고 재부팅 해준다.

제대로 설치됐는 지 확인방법: `im-config -n fcitx5`
    - im-config: input framework 설정
    - -n: 대화형 메뉴 없이 지정한 값(fcitx5)으로 설정
제대로 바뀌었는 지 확인방법: `ps -ef | grep fcitx`
    - ps -ef: 현재 실행중인 모든 프로세스를 자세히 출력 (-e: 전체프로세스, -f:자세히)
    - |(pipe): 앞 명령어 결과를 뒤 명령어로 넘김
    - grep fcitx: 출력된 내용 중 fcitx라는 문자열이 포함된 줄만 필터링

## Key Mapping

- 한/영 키가 ALT로 눌리는 문제 해결 방법

1. `xev` 실행. 아래 그림에서 보이는 흰색 창을 클릭하고 바꾸려는 키(한/영 키) 클릭 -> keycode 확인. (아래에선 108)
![ubuntu xev result](ubu_xev.png)
2. 108번 키를 한/영키로 설정:
    ```xmodmap -e "keycode 108 = Hangul"```
2.5 바뀌었는 지 확인해보기
3. `xmodmap -pm`은 modifier를 확인하는 코드. ALT_R이 있는 지 확인
    - modifier: 다른 키의 의미를 바꾸는 보조 키
    - 예시) Shift(누르면 다른 키 대문자/기호 됨), Ctrl/Alt(단축키), Super/Win(시스템 단축키)
4. 있다면 지우기:
    ```xmodmap -e "remove mod1 = Meta_R Alt_R"```
    - Meta: 옛날 UNIX 키보드에 있던 별도 키. 요즘은 사라지고 Alt나 Win키로 대체됨. 어떤 시스템에선 Alt_R이 아니라 Meta_R로 등록돼있을 수도 있어서 둘 다 제거하는게 맞음.
5. Keycode에 ALT 기능 완전 제거 후 Hangul 만 지정: 
    ```xmodmap -e "keycode 108 = Hangul NoSymbol Hangul"```
    - 첫 번째 자리의 Hangul: 그냥 눌렸을 때 한/영키로 작동해라
    - 두 번째 자리의 NoSymbol: Shift누르고 눌렸을 때 아무 동작 하지 마라
    - 세 번째 Hangul: 다른 상태들에선 한/영키로 작동해라

이 것들을 모두 진행한 후 한/영 키가 정상 동작했다.



## 이후 설정

재부팅 후 한/영 전환이 Hangul키로 안됐는데 아래 사진처럼, 상단바 키보드 버튼에서 configure를 누른 다음, Global Options에서 Hangul이 원래 되어있었지만, 지우고 다시 Hangul로 한 다음 Apply눌러주니 다시 돌아왔다.
![keyboard configure button](ubu_keyboardConfigure.png)
![fcitx configure menu](ubu_fcitxconfig.png)
## 여담

한영전환이 느린건 해결됐는데, 한국어 입력이 느린 것은 해결이 안됐다.
무조건 느린 건 아니고, Chrome Chat GPT에서만 느렸다. 이건 Firefox에서 ChatGPT를 이용하는 방법으로 해결했으나 원인은 찾지 못했다..