---
layout: wiki
title: Communication API
toc: true
---

커뮤니케이션 API는 HTML5뿐만 아니라 관련 API에서도 폭넓게 채용되어, 여러 프로그램 간에 비동기 방식으로 메시지를 주고받아 느슨한 결합(Loosely-Coupled) 데이터를 공유할 수 있게 됨. 여기서 말하는 메시지란 JavaScript 객체 혹은 단순 문자열.

### MessageEvent 인터페이스
* data: 송신되는 메시지의 내용이 되는 데이터
* origin: 메시지 송신처의 도메인(크로스 도큐먼트 메시징과 Server-Sent Events에서만 사용됨)
* lastEventId: 마지막 이벤트(Server-Sent Events에만 사용됨)
* source: 메시지를 보내는 윈도우 객체(크로스 도큐먼트 메시징에서만 사용됨)
* ports:메시지 송신 시 지정한 포트의 복사본(여러 개)(크로스 도큐먼트 메시징과 채널 메시징에서만 사용됨)

### 크로스 도큐먼트 메시징

### 채널 메시징

### 포트 공개
