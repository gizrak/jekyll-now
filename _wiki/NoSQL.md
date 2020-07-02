---
title: NoSQL
---

## NoSQL의 개요

### NoSQL의 정의
* 기본개념: <http://egloos.zum.com/calmglow/v/4580668>
* NoSQL에 대해서 알아보자: <https://embian.wordpress.com/2013/06/27/nosql-2/>

### NoSQL의 등장배경
1. 데이터 규모의 확대
  - 저장할 데이터가 많아지면서 읽고/쓰기에 있어서 RDB가 제약 요소가 되었다.
  - RDB의 수평적 확장성 한계로 새로운 해결책이 필요했다.
1. 웹 서비스의 구조 변화
  - 저장할 데이터의 형태가 계속 변화한다.
  - 사용자의 데이터 요구가 일관적이지 않고 다양하다.

## NoSQL의 종류

### 맵+엉성+다차원
* memcache
* 메모리 DB 형태로 Key-Value 구조로 되어 있음
* 해싱기법에 의해 다중 서버로 관리
* 캐시 용도로 많이 사용

### 맵+엉성+다차원+분산
* 오라클 coherence, IBM ObjectGrid
* memcached에 그리드 기반 기술을 접속
* 메모리만 충분히 많다면 가장 빠른 처리시스템을 보유할 수 있고 데이타 복제나 분산기반 확장등에 아주 많은 잇점을 가져올 수 있음
* 별도의 솔루션을 이용하면 일반 Disk기반의 영속성등을 처리 가능

### 맵+엉성+다차원+분산+영속성+정렬
* HBase, BigTable, Cassandra
* 기본적인 NoSQL 기능을 대부분 가짐
