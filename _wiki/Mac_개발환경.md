---
title: Mac 개발환경
---

Mac은 brew와 같은 CLI 기반의 패키지 관리 도구 덕분에 개발환경을 구축하기 편하다. 여기에 iCloud를 사용하면 로컬 환경을 간편하게 클라우드 환경으로 옮겨놓을 수 있다.

## 출발하기

## brew 설치

내가 Mac이나 Linux로 개발하다가 Windows 환경을 다시 못돌아가는 이유가 2가지 있는데, 하나는 터미널이고 나머지 하나가 패키지 관리자이다. 터미널은 Windows에서 PowerShell을 지원하면서~~맘에는 안들지만~~ 어느 정도 해결은 되었다. 그런데 Windows에선 아직 쓸만한 패키지 관리자를 보진 못했다.

{% include figure image_path="/assets/images/wiki/mac_terminal.jpg" alt="Mac 터미널" caption="나의 최애템 Mac 터미널 환경" %}

레드햇 리눅스에서는 rpm에서 업그레이드 된 yum을 사용하고, 데비안 계열의 우분투 리눅스에서는 dpkg에서 업그레이드 된 apt를 사용한다. 리눅스에서는 [port](https://www.macports.org/)와 [brew](https://brew.sh/) 2가지 선택지가 있는데, 둘의 차이는 소스를 직접 빌드하거나 혹은 이미 빌드된 바이너리를 그냥 받느냐이다. yum, apt와 마찬가지고 그냥 바이너리를 다운받는 brew가 빠르고 더 편리하다.

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

## zsh 환경 구축

## 개발 환경

## Java

## Python

## Ruby

## 클라우드

## iCloud 저장소 설정

## 로컬 파일 symbolic link 생성

## 기타 환경

## Archery

