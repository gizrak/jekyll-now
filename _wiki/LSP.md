---
layout: wiki
title: LSP
---

`Liskov Substitution Principle`

### 리스코프 대체 원칙의 개요
#### 리스코프 대체 원칙의 정의
> 객체지향 5대 원칙(SOLID) 중 하나로 기반 클래스는 서브 클래스로 대체되는 IS-A 관계가 성립해야 한다는 원칙

#### 리스코프 대체 원칙의 전제조건
* Pre-Condition: Base class 보다 조건이 까다로운 pre-condition이 있으면 안됨
* Post-Condition: Base class 보다 조건이 부족한 post-condition이 있으면 안됨
* Derived method는 Base method와 동일해야 함

### 리스코프 대체 원칙의 설계 원칙
![](http://cafefiles.naver.net/data30/2008/6/22/15/lsp_01_lsymir.jpg)

### IS-A 관계에 대한 경험적 설계 법칙
1. 만약 Base 클래스와 Derived 클래스가 똑같은 일을 한다면 구분 필드 이용한 클래스로 표현
1. 똑같은 연산을 제공하지만, 이들을 약간씩 다르게 구현한다면 공통의 인터페이스를 만들고 이를 구현
1. 공통된 연산이 없다면 완전 별개인 2개의 클래스를 생성
1. 만약 Derived 클래스가 추가적으로 무언가를 더 구현한다면 구현 상속을 사용

### 참조
<http://blog.naver.com/PostView.nhn?blogId=kcufl&logNo=60063753537&parentCategoryNo=18&viewDate=&currentPage=1&listtype=0>
