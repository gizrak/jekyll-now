---
title: IPS
category:
  - Security
---

`Intrusion Prevention System`

## IPS의 개요
### IPS의 정의
> 네트워크 구간, 서버, 호스트에 설치되어 패킷의 Payload를 패턴 기밤 탐지를 통해 유해 트래픽을 차단하는 장비 또는 기술

### IPS의 특징
* 패킷 데이터 검사: 방화벽은 헤더 정보만 기반으로 처리
* 탐지와 차단: IDS(Intrusion Detection System)는 탐지만 가능

### IPS 종류
* Network IPS: 네트워크 구간에서 방화벽의 앞 또는 뒤에 설치
* Host IPS: 각 운영체제에 소프트웨어 형식으로 설치

## IPS 주요 기능
### IPS 패턴 종류

|분류|상세 설명|
|---|-------|
|오용탐지(Signature Base) |Signature 기반으로 알려진 공격을 차단 |
|이상탐지(Anomaly Detection) |정상적인 트래픽이지만 임계치 이상의 트래픽 유입 시 차단 |

### IPS 오탐

|분류|상세 설명|
|---|-------|
|False Positive |정상적인 트래픽을 공격으로 오인하여 탐지, 차단 |
|False Negative |공격, 유해 트래픽을 정상 트래픽으로 오인하여 허용 |
