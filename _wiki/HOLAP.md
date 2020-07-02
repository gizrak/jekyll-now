---
title: HOLAP
---

`Hybrid OLAP`

## HOLAP의 개요
### HOLAP의 정의
DW 환경에서 대용량 데이터의 접근성과 신속한 Cube 분석을 통한 의사결정을 동시에 지원하는 사용자 관점의 데이터 분석 및 활용 도구

### HOLAP의 등장배경
- ROLAP: 용량 우선
- MOLAP: 성능 우선
- 용량과 성능을 균형있게 지원하는 도구 필요

## HOLAP의 아키텍처 및 기술
### HOLAP의 구성 아키텍처
![](http://image.slidesharecdn.com/olapbybharatkalia-140909030348-phpapp02/95/olap-basics-and-fundamentals-by-bharat-kalia-66-638.jpg?cb=1410231895)

|구성|설명|
|---|---|
|Multi Dimension Cube |Dimension hierarchies, Cube lattice, 빠른 응답속도 보장 |
|Rational cube |관계형 Database 내 구축, 확장성, 메타 데이터 활용, 스타스키마/스노우플레이크 |
|2-way Approach |Detail Data는 SQL 활용, Aggregated Data는 MOLAP Tool 활용 |

### HOLAP의 핵심 기술

|구분|기술|설명|
|---|---|---|
|Fast query Performance |Cube processing |Sorting aggregation, rollup, drill down, pivot, slice dice |
| |Pre computing |많은 Set의 dimention 미리 저장, 실시간 접근 |
|High data capacity |Rational database |대용량 data volume 지원, 확장성 보장, 유연한 구조 |
| |Scheme/Index |Star scheme/snowflake, bitmap index, multi table join |

## HOLAP과 타 OLAP 비교

|항목|HOLAP|MOLAP|ROLAP|
|---|-----|-----|-----|
|구조|혼합|Multi Dimensional DB|RDBMS|
|장점|혼합|실시간 분석|사용성,확장성,대용량|
|기술|Vertical/Horizonal Partitioning|다차원 큐브|눈송이/스노우플레이크 스키마|
|사례|Microsoft|Pilot,Gentia,Arbor Essbasee|Oracle,Sybase,Informix|
