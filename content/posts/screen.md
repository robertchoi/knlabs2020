---
title: "리눅스에서 screen 명령어의 사용"
date: 2020-01-30T22:33:42+09:00
draft: false
tags: ["Linux", "Command", "리눅스", "명령어"]
categories: ["Linux"]
---

## Screen이란?
Screen이란 Linux에서 물리적인 터미널을 여러 개의 가상 터미널로 다중화해주는 도구입니다. 각 가상 터미널은 독립적으로 동작하며 사용자 세션이 분리되어도 동작합니다. 간단히 말하면 이 도구는 백그라운드로 동작하는 다중 터미널을 만들어 줍니다. 이걸 이용해서 백그라운드 작업을 간단히 수행할 수도 있고 회사에서 작업하던 터미널 화면을 집에 가서도 같은 터미널 화면을 보며 작업을 이어 할 수도 있습니다.

## 설치
- RedHat계열 (RedHat, CentOS, Fedora 등...)
```
yum install screen
```

- Debian 계열(Ubuntu 등..) #
```
apt-get install screen
```

## 사용법
### 추가 환경 설정
아래와 같이 설정 파일을 추가해주면 Screen 사용 시 좀 더 편해집니다. 적용하시는 것을 추천합니다. 각 가상 터미널의 창 구분도 되고 시계도 표시되는 등 더 보기 편해집니다.
```
vim ~/.screenrc
```

```
defscrollback 5000
termcapinfo xterm* ti@:te@
startup_message off
hardstatus on
hardstatus alwayslastline
hardstatus string "%{.bW}%-w%{.rW}%n*%t%{-}%+w %= %c ${USER}@%H"
bindkey -k k1 select 0
bindkey -k k2 select 1
bindkey -k k3 select 2
```

### screen 진입과 탈출
- screen 진입
  * screen : 일반적인 진입
  * screen -S [세션이름] : screen세션 이름을 지정하여 실행
  * screen -r [세션이름] : 실행중인(Detached) screen 세션으로 재 진입시 실행하는 명령어, screen세션이 하나만 실행중일 경우 세션이름을 입력하지 않아도 진입이 된다.
  * screen -x [세션이름] : 실행중인(Attached) screen 세션으로 재 진입시 실행하는 명령어, screen세션이 하나만 실행중일 경우 세션이름을 입력하지 않아도 진입이 된다.

- screen 탈출 
  screen을 종료 시키기 위해서는 모든 터미널을 종료(exit)하면 된다. screen 세션을 유지한 상태에서 나오기를 원한다면 Ctrl + a, d를 입력하면 된다.

### screen 명령어
Screen에서의 명령은 Ctrl + a 와 다른 키의 조합으로 이루어진다. 먼저 Ctrl + a를 누른 후 조합키를 누르면 된다. 동시에 누르는 것이 아니고 순차적으로 눌러야 한다.
  * Ctrl+a, c : 새창 띄우기
  * Ctrl+a, a : 바로 전 창으로
  * Ctrl+a, n : 다음 창으로
  * Ctrl+a, p: 이전 창으로
  * Ctrl+a, 스페이스 : 다음 창으로
  * Ctrl+a, 백스페이스 : 이전 창으로
  * Ctrl+a, 0 : 0번째 창으로
  * Ctrl+a, 1 : 1번째 창으로
  * Ctrl+a, 9 : 10번째 창으로
  * Ctrl+a, d : screen 탈출(screen은 계속 실행중이다.)

## 참조문헌
[Linux screen 사용법](https://dreamlog.tistory.com/470)
