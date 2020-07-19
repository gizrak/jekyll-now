---
title: DNSSEC
category:
  - Network
---

`DNS Security Extensions`

## DNSSEC의 개요
### DNSSEC의 정의
[DNS](/wiki/DNS)에 대한 신뢰성을 인증하고 송수신 데이터에 대한 무결성을 제공하기 위해 IETF를 중심으로 만들어진 DNS 확장 표준 프로토콜

### DNSSEC의 원리
DNS 응답 정보에 전자서면 값을 첨부하여 보내고, 수신측이 해당 서명 값을 검증함으로써 DNS 위변조를 방지하고 정보 무결성을 제공하는 매커니즘

![](https://www.icann.org/sites/default/files/unmanaged/images/dnssec-home-graphic-680x284-13feb12.png)

## DNSSEC의 매커니즘과 리소스 레코드
### DNSSEC의 정보 제공자 매커니즘
1. 서명용 키쌍을 생성하여 공개키는 사전에 배포
1. 개인키를 가지고 자신이 제공하려는 정보(도메인 정보 등)의 해쉬값을 서명 처리하여 [전자서명](/wiki/전자서명) 값을 생성
1. 원본데이터와 추가된 전자서명값을 함께 인터넷 상에 제공

### DNSSEC의 정보 이용자 매커니즘
1. 정보 제공자로부터 수신한 정보의 원본 데이터와 전자서명값을 분리
1. 사전에 정보 제공자로부터 수신한 공개키값을 가지고 전자서명값을 복호화
1. 원본 데이터를 해쉬처리한 값과 앞서 복원한 전자서명값을 비교, 일치 여부를 확인

### DNSSEC의 리소스 레코드(RR)

|원리|이름|설명|
|----|----|----|
|RRSIG|Resource Record Signature RR|도메인네임 시스템의 각 리소스 레코드 데이터에 대한 전자서명 데이터를 저장하기 위한 리소스 레코드|
|DNSKEY|DNS Publickey RR|도메인존(zone)의 공개키 데이터를 저장하여 제공하기 위한 리소스 레코드|
|DS|Delegation RR|DNS 고유의 위임체계에 따라 보안측면의 인증된 위임체계를 구성하기 위한 데이터를 저장하기 위한 리소스 레코드|
|NSEC|Next Secure RR|DNSSEC가 제공하는 보안기능 중 'DNS 데이터의 부재인증(authenticateddenial os existence of DNS data)'을 위해 정의된 리소스 레코드|

## DNS 보안 취약점

|종류|내용|
|----|----|----|
|DNS 캐시 포이즈닝 공격|DNS 정보를 위변조하는 공격<br>DNS 프로토콜 자체의 취약성으로 DNS 캐시에 저장된 쿼리 정보를 위변조|
|패킷 가로채기|DNS 질의/응답 과정 중의 패킷을 가로채 정보 위변조|
|정보제공 DNS로 위장 공격|루트 네임서버, KR 네임서버 등 정보제공 DNS로 위장하여 잘못된 정보를 제공|
