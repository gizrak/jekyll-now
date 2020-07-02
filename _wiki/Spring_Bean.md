---
title: Spring Bean
---

## Definition
* Spring에서 사용되는 [POJO](/POJO.md)
* Spring IoC(Inversion of Control)로 인스턴스화, 관리, 생성되는 객체
* 주요 속성
  * class(필수): 정규화된 자바 클래스 이름
  * id: bean의 고유 식별자
  * scope: 객체의 범위 (sigleton, prototype)
  * constructor-arg: 생성 시 생성자에 전달할 인수
  * property: 생성 시 bean setter에 전달할 인수
  * init method와 destroy method

## Bean Scope

| Scope | Description |
| -------- | -------- | -------- |
| singleton | 하나의 Bean  정의에 IoC 컨테이너 내 하나의 객체만 존재 |
| prototype | 하나의 Bean 정의에 대해 다수의 객체가 존재 |
| request | 하나의 Bean 정의에 대해 HTTP request 생명주기 내 하나의 객체만 존재 |
| session | 하나의 Bean 정의에 대해 HTTP session 생명주기 내 하나의 객체만 존재 |
| global session | 하나의 Bean 정의에 대해 global HTTP session 생명주기 내 하나의 객체만 존재 |
