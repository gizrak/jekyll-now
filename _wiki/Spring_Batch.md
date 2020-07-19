---
title: Spring Batch
category:
  - Language
---

## Batch

* 대용량 데이터: 대량의 데이터를 I/O
* 자동화: 사용자의 개입 없이 실행
* 견고성: 실행 도중 종료되는 일 없이 수행
* 신뢰성: 중복이나 누락 없이 수행
* 성능: 대량의 데이터를 유의미한 시간 안에 수행

## Spring Batch
* @Configuration 등록 필요
* Job: 하나의 배치 작업 단위
* Step: Job에 속한 하위 작업 단위 (기본 트랜잭션)
  * Tasklet: Custom 작업을 처리하기 위한 단위
  * Reader
  * Processor
  * Writer

## 메타 데이터
* spring-batch-core.jar 내부에 `schema-*.sql` 파일이 존재
* `BATCH_JOB_INSTANCE`: Job Parameter에 따라 record 생성됨
* `BATCH_JOB_EXECUTION`: Job Instance의 자식 관계로 실행마다 record 생성됨
* `BATCH_JOB_EXECUTION_PARAMS`
* `BATCH_JOB_EXECUTION_CONTEXT`
* `BATCH_STEP_EXECUTION`
* `BATCH_STEP_EXECUTION_CONTEXT`

## Scope
* [Bean](/wiki/Bean)의 생성 시점을 지정된 Scope가 실행되는 시점으로 지연
* `@JobScope`: Step 선언문에서 사용
* `@StepScope`: Tasklet이나 Reader/Processor/Writer에서 사용
* 장점
  * JobParameter의 Late Binding
  * 동일한 컴포넌트의 병렬 접근

## Chunk

## ItemReader

## ItemWriter
