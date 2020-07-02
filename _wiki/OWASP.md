---
title: OWASP
---

## OWASP IoT Top 10의 개요
### OWASP IoT Top 10의 정의
IoT 취약점 중 공격 빈도가 높으며, 보안상 큰 영향을 줄 수 있는 10가지 취약점 대응방안 가이드

### OWASP IoT Top 10의 개념도
![img](http://image.slidesharecdn.com/2015appsecusav1-150918180933-lva1-app6891/95/owasp-appsec-usa-2015-san-francisco-43-638.jpg?cb=1442869027)

## OWASP IoT Top 10의 주요 항목

|주요 항목|설명|
|-------|---|
|Insecure Web Interface|초기 설정 시 기본 비밀번호 및 사용자명을 변경하지 않거나 단순한 비밀번호 사용 등 OWASP Top 10 취약점이 노출된 상태|
|Insufficient Authentication/Authorization|견고하지 않은 비밀번호 복구 매커니즘과 단순한 암호, 세분화 되지 않는 접근의 권한 부여|
|Insecure Network Service|불필요한 포트의 노출과 버퍼 오버플로우 및 퍼징 공격에 취약한 서비스, 장비 및 사용자들에게 영향을 주는 DoS에 취약한 서비스|
|Lack of Transport Encryption|SSL/TLS 같은 프로토콜이나 기타 다른 산업 표준 등 암호화기술 사용하지 앟는 데이터 전송|
|Privacy Concerns|개인정보를 보관하는 장비와 구성요소의 부적절한 보호, 암호화되지 않고 무분별하게 수집하는 개인정보|
|Insecure Cloud Interface|부적절한 계정 처리(계정잠금 횟수, 비밀번호 재설정 매커니즘 등)와 무선 네트워크를 통한 인증정보 노출|
|Insecure Mobile Interface|부적절한 계정 처리(계정잠금 횟수, 비밀번호 재설정 매커니즘 등)와 무선 네트워크를 통한 인증정보 노출|
|Insufficient Security Configurability|일반 사용자와 관리자와의 혼환된 보안구성, 암호화되지 않는 데이터 전송, 강력한 비밀번호 강제 정책 부재|
|Insecure Software/Firmware|암호화하지 않는 업데이트 파일의 암호화하지 않는 파일전송과 업데이트 파일의 서명 미확인|
|Poor Physical Security|쉽게 분해 가능한 장치와 악의적 접근가능한 USB 포트 등 외부 포트 존재, 쉽게 제거 가능한 데이터 저장 매체, 암호화하지 않는 데이터 저장장치|
