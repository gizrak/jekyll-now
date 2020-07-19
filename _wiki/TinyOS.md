---
title: Tiny OS
category:
  - Computer
---

## Tiny OS 개요
### Tiny OS의 정의
* UC 버클리에서 개발된 센서 네트워크를 위한 무료 운영체제
* HW, MAC 프로토콜, Network 프로토콜, 센서 I/F를 완전 공개한 작은 사이즈의 OS

### Tiny OS의 용도
* 저전력, 저용량의 시스템에서 사용
* 임베디드 환경에서 센서 네트워크 구성 시 사용

## Tiny OS의 구성도
### Tiny OS의 구성요소
일반 OS 관점의 커널과 드라이버, 그리고 Tiny OS 특화된 센서 및 통신 드라이버를 포함

|분류|구성요소|설명|
|----|--------|----|
|HW 영역|Wireless Driver|RF 무선 통신을 위한 표준 기술<br>Bluetooth, zigbee 등|
| |Sensor Driver|센서처리를 위한 HW, accelerometer, gyro 센서 등|
|SW 영역|OS Kernel|센서처리, 무선통신 처리, 스케쥴 처리|
| |응용 SW|컴포넌트 기반으로 동작<br>한번에 하나의 Application만 서비스 가능|

### Tiny OS의 구성도
![](http://cfile23.uf.tistory.com/image/17519F404E93D8F8027CE7)

## Tiny OS 스케쥴링 방식
* Event Driven 구조
* FIFO 형태의 스케쥴러로 동작 (전원이 꺼질 때까지 무한루프)

|동작유형|설명|
|--------|----|
|Loop|Task Queue Empty가 Task나 Event 있는지 확인|
|Sleep|Task나 Event 없는 경우 Sleep|
|Event 발생|HW 인터럽트 이벤트 발생하고 sleep 진입|
|Task 발생|Queue에 Task 등록되고 Task 수행|
