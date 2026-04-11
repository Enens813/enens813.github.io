---
layout: post
title: Ubuntu - Mac 원격접속
date: 2026-04-04 22:40 +0900
categories: [Basics]
tags: [ubuntu, mac, remote, control]
description: 우분투에서 mac으로 원격접속 하는 방법 설명
---

## 개요

맥 환경에서 개발하고 24시간 돌리기 위해 맥 미니를 샀지만, 매번 들고다니기엔 번거로웠다. 그래서 맥북을 따로 사지 않고 잘 쓰고 있는 노트북에서 원격접속으로 사용하려 했다. 마침 노트북 윈도우가 학교를 졸업하면서 더이상 못 쓰게 되어 노트북은 우분투로 설치하고 우분투에서 맥 미니로 원격접속 하는 방법을 설명하려 한다.

가장 쉽게는 chrome remote control을 쓸 수 있지만, mac은 키보드가 달라서 그걸 설정할 수 있고, 더 고해상도와 저지연을 가능하게 하는 소프트웨어를 찾아야 했다. 이걸 위해선 두 가지가 필요한데,


1. 집에 있는 mac과 여기저기 들고다닐 ubuntu가 같은 network안에 있어야 한다. -> tailscale
2. 저지연, 고해상도로 원격 접속을 지원하는 소프트웨어가 있어야 한다 -> nomachine


## Tailscale

#### Mac

1. tailscale 홈페이지 찾아서 들어가서 설치
2. tailscale 회원가입 및 로그인
3. terminal에 `tailscale ip` 입력해서 ip 확인
4. terminal에 `whoami` 입력해서 user name 확인
5. 설정 > 일반 > 공유 > Screen Sharing, Remote Management ON
6. tailscale 켜기

#### Ubuntu

1. tailscale 홈페이지 찾아서 들어가서 설치
2. terminal에 `sudo tailscale up` 해서 tailscale 켜주기
3. 맥에서 했던 것과 같은 아이디로 로그인 하면 완료


## Nomachine


#### Mac

1. NoMachine 홈페이지 들어가서 설치

#### Ubuntu

1. NoMachine 홈페이지 들어가서 deb으로 설치 (tar.gz로 설치하려 했는데 뭐가 잘 안돼서..)
2. app icon 찾아서 GUI로 실행하면 로컬 네트워크에 있는 다른 컴퓨터를 알아서 찾는다.
2-1. 만약 이 때에도 mac이 다른 네트워크에 있고 tailscale로 연결된 상태라면, 수동으로 Add 해서 'Add Connection' 누르고, Host에 Mac의 tailscale ip, Port 4000, Protocol NX로 해서 직접 해줘야 한다.


## 화면, 키보드 설정

나는 삽질 좀 했지만 위까지 하는 건 별거 없다. 그치만 이 키보드 설정에서 더 삽질했다.. 그걸 정리해보면,

1. Ubuntu에서 NoMachine으로 Mac에 들어간다
2. ctrl+alt+0를 눌러서 환경설정 화면으로 들어간다.
3. 우선 Display로 들어가서 ㄴㅇㄹㄴㄹㅇㅇㄹㄴㅇㄴㄹㄴ
사진
4. input으로 들어가서 'Grab the keyboard input'과 'Map Ctrl to Cmd and Super to Ctrl'을 선택한다
![NoMachine Input Setting](image.png)
    - super는 윈도우 버튼이자, Cmd 버튼이다.
    - 이걸 선택하면 키보드의 ctrl을 눌렀을 때 맥에서 cmd를 누른 효과를 얻는다.

위 방식대로 따라하면 cmd는 쓸 수 있었지만 한영전환이 안 됐다. 그래서 한영전환을 따로 해줘야 한다.

1. 우분투 키보드에서, mac에서 입력이 안되는 것처럼 보이는 버튼들을 눌러보며 어떤 키로 입력이 되는 지 찾아본다.
    - 이건 우연인데.. 나는 원격접속 상태에서 ubuntu키보드의 한/영 키를 두번 눌렀을 때 Mac의 Claude가 실행되는 걸 확인했고, Claude의 실행 단축키가 option 키 두번 인 걸 찾아내어, 한/영 키를 눌렀을 때 option 키가 눌린다는 걸 알아냈다.
2. Mac에 연결된 키보드도 windows용 키보드여서 option 키가 없었다.. 그래서 Mac에 karabiner-elements를 설치했다.
3. karabiner-elements와 karabiner-monitoring을 실행할 때 맥 설정에서 여러가지 허용해줘야 하는데, 팝업 뜨는거 대로 따라해주면 된다. 팝업을 막 지우지 말자.
4. karabiner-monitoring을 실행하고, Mac에서 입력이 안 되던 내 windows용 키보드 버튼을 클릭해서 뭐가 뜨는 지 확인한다. (나는 '한/영' 키를 눌렀을 때 'japanese-kana'가 떴다. 참고로, Ubuntu 컴퓨터에서의 입력은 karabiner로 들어가지 않는다.)
5. karabiner-elements에서 'Complex Modification'을 들어가서 아래처럼 'japanese-kana'를 'option'으로 바꾸도록 설정한다. 
```
{
    "description": "Map japanese_kana to option",
    "manipulators": [
        {
            "type": "basic",
            "from": {
                "key_code": "japanese_kana"
            },
            "to": [
                {
                    "key_code": "left_option"
                }
            ]
        }
    ]
}
```
6. Mac의 설정 > 키보드 > 단축키 > 입력 형식에서, 한영 전환 단축키를 option + Space로 바꿔준다. (보통 다들 +space를 붙여서 한영전환하는 것 같아서..)
7. 그럼이제 Ubuntu에서 한/영 + Space를 누르면 Mac에서 한/영 전환이 된다!!

자 근데 이제 또 Ubuntu의 한/영키가 안 먹기 시작했다. 그건 다음 포스팅에 이어서..


## 그럼이제?

1. 우분투를 켜서 terminal에 `tailscale up` 을 쳐서 mac과 같은 네트워크에 있게 한다.
2. NoMachine으로 들어가서 Mac mini를 더블클릭

## 다음 포스팅 예정
Ubuntu 한/영키 정상화
Ubuntu - Mac 파일 전송 