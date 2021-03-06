---
title: Secure OS
category:
  - Computer
---

## Secure OS의 개요
### Secure OS의 정의
> 서버나 PC 환경에서 운영체제 자체에 내재된 보안상 결함으로 부터 시스템을 보호하기 위해 기존 운영체제에 추가 설치하는 보안 기능이 강화된 커널 레벨의 보안 소프트웨어

### Secure OS의 등장 배경
1. 방화벽, IPS와 같은 네트워크 레벨 보안의 한계
1. root, administrator와 같은 관리자 계정 탈취로 인한 문제점
1. 운영체제 자체의 보안 취약점으로 인한 제로데이 공격

### Secure OS의 특징
* 운영체제 레벨에서의 해킹 차단: 운영체제 수준에서 강력한 접근제어를 통해 주요 파일의 불법적인 변조, 탈취 등을 차단하고, 불법적인 root 권한 획득, Daemon에 대한 공격, 시스템 파일 변조, 불법 실행파일을 통한 해킹 시도 등을 차단하여 악의적인 공격으로부터 시스템을 보호할 수 있음
* TCSEC B1 등급의 보안 기능 구현: 미국 국방성의 평가기준인 TCSEC의 B1 등급에서 요구하는 보안 기능(다중등급보안, 강제적 접근제어 등)에 맞게 시스템을 구현할 수 있음
* 통합 보안관리 환경 구현: 다수의 서버에 대한 보안 관리를 중앙에서 원격으로 수행할 수 있기 때문에 체계적인 보안관리가 가능함
* 시스템 자원 분리: 웹 서버, 웹 페이지, 애플리케이션 파일, 시스템 파일 등을 서로 다른 보안 영역으로 분리함으로써 악의적인 침입에 따른 추가적인 공격을 차단할 수 있음

## Secure OS의 구성 및 기술
### Secure OS의 구성도
![](http://cfile2.uf.tistory.com/image/182F1F0E49E493570A1E6C)

### Secure OS의 주요 기능
##### 간단한 분류

|주요 기능|상세 설명|
|-------|------|
|사용자 식별/인증|운영체제에 접속하는 계정이 누구이고 사용 권리가 있는지 확인하는 기능 |
|접근 제어|컴퓨터 HW, 파일, 디렉토리 등의 리소스의 접근을 허용/차단하는 기능 |
|침입 탐지/방어|운영체제 보안 취약점 또는 악성코드 등으로부터 운영체제를 보호하는 기능 |

##### 상세화된 분류

|주요 기능|상세 설명|
|-------|------|
|Unix의 superuser(root)의 취약성 제거|인증된 사용자라도 일체의 권한이 없는 시스템 자원에 대한 접근을 허용하지 않아야 합니다. |
|등급기반 접근통제시스템(Label-based Access Control System)|모든 컴퓨터 자원(주체와 객체)에 보안등급을 부여하여 강력한 보안정책을 적용할 수 있어야 합니다. |
|강제적 접근제어(MAC : Mandatory Access Control)|정보 및 사용자의 보안등급에 기반하여 정보에 대한 접근을 통제할 수 있어야 합니다. |
|시스템 자원의 엄격한 분리|상용 소프트웨어의 버그를 이용한 침입을 차단하며 일정 영역에 대한 침입에 성공했을지라도 다른 어플리케이션 또는 권한이 없는 영역에 대한 추가 공격을 불가능하게 해야합니다. |
|엄격한 보안 감사, 추적|보안과 관련된 모든 행동의 책임추적이 가능하도록 보안관련 사건을 기록 및 유지해야 하며, 기록된데이터를 검토할 수 있는 수단을 제공해야 합니다. |
|데이터보호|저장된 데이터 혹은 신뢰할 수 있는 데이터를 인가되지 않은 노출, 변경, 삭제로부터 보호해야 합니다. |
|운영체제보강|운영체제상의 필요하지 않은 서비스나 수단 등은 모두 제거하는 작업을 통해 운영체제상의 취약점에 대한 보강작업이 수행되며, 운영체제에 대한 신뢰성과 안정성이 보장되어야 합니다. |

## Secure OS의 도입 시 고려사항
1. 대상 시스템의 선정: 어떤 목적으로 어떤 시스템에 적용을 할 것인가 ?
1. 보안정책 사전 수립: 서버보안을 이용하여 어떤 보안정책을 적용할 것인가 ?
1. 전담 관리자의 선정: 여러대의 시스템을 관리할 보안관리자가 없는 경우 지속적인 관리등 이 어려움.
1. 안정성/호환성 고려: 서버보안은 커널레벨의 제품으로 기 운영중인 시스템에 영향을 주지 않아야 함. 이미 운영중인 어플리케이션과 충돌이 없어야 합니다.
