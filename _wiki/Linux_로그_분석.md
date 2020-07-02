---
title: Linux 로그 분석
---

|명령어|설명|
|----|---|
|aculog|Dial-out 모뎀 사용 내역|
|history|사용자별 명령어|
|lastlog|사용자 최근 로그인 시간|
|loginlog|실패한 로그인 시도|
|maillog|메일 시스템 수행 내역|
|messages|부팅시의 시스템 콜솔 내용|
|secure|시스템 권한 관련 로그|
|sulog|su 명령 사용 내역|
|utmpx|현재 로그인한 사용자 내역|
|vold.log|외부 매체 사용에 대한 에러|
|wtmpx|사용자의 로그인, 로그아웃 시간|
|xferlog|ftp 사용 내역|

로그 파일을 검사할 때는 주로 messages, last, secure등의 로그를 살펴 외부에서 공격한 공격로그가 남아있는지, 관리자가 추가하지 않은 사용자가 접속한 흔적은 있는지, 특정한 서비스에 접속한 흔적 등이 있는지 확인해 보아야 한다.

예) 버퍼오버플로우 공격을 받을 때 messages에 남는 로그

```
Jan 15 09:16:53 roo1-03 rpc.statd[838]: gethostbyname errorfor
^X??X??Z??Z??8x%8x%8x%8x%8x%8%62716x%hn%51859x%hn\
220\220\220\220\220\220\220\220\220\220\220\220\220\220\220\220\
220\220\220\220\220\220\220\220\220\220\220\220\220\220\220\220\220\
```

예) 관리자가 추가하지 않은 사용자가 접속해 secure에 남은 로그

```
Feb 3 00:23:54 localhost sshd[1515]: Accepted password for amc from 80.97.191.237 port 1145
Feb 3 02:04:27 localhost sshd[1662]: Accepted password for amc from 80.97.158.154 port 59786
Feb 3 02:19:12 localhost sshd[1842]: Accepted password for amc from 80.97.158.154 port 59891
Feb 3 05:48:36 localhost sshd[3149]: Accepted password for amc from 80.97.158.154 port 41685
Feb 3 06:08:20 localhost sshd[3301]: Accepted password for amc from 80.97.158.154 port 41698
Feb 3 23:07:03 localhost sshd[8532]: Accepted password for amc from 80.97.191.142 port 1334
```
