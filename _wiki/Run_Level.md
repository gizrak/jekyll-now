---
title: Run Level
---

시스템 관리의 용이함을 위하여 서비스의 실행을 단계별로 구분하여 적용하는 것

|레벨|이름|내용|
|---|---|---|
|0|halt|시스템 종료|
|1|Single user mode|시스템 복원모드. 관리자 권한 쉘을 얻게됨|
|2|Multiuser mode|NFS(Network File System)을 지원하지 않는 다중 사용자 모드<br>Network 기능을 사용하지 않는다면 3과 동일|
|3|Full multiuser mode|일반적인 쉘 기반의 인터페이스를 가진 다중 사용자 모드|
|4|unused|기본적으로 쓰이지 않으나 임의로 정의해서 사용할 수 있음|
|5|X11|기본적으로 3과 동일하나 Graphic User Mode라는 점이 다름|
|6|reboot|시스템 재부팅|
