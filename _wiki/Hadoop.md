---
title: Hadoop
category:
  - Data
---

대량의 자료를 처리할 수 있는 큰 컴퓨터 클러스터에서 동작하는 분산 응용 프로그램을 지원하는 자유 자바 소프트웨어 프레임워크

## Hadoop의 개요
### 왜 쓰는가?
- map()과 reduce()만 오버라이딩: 로직을 구현한다
- 나머지 병렬처리/분산처리/클러스터링 부분은 Hadoop이 처리함
- Xaas: SaaS, DaaS, IaaS, PaaS
- Big Data 이전 Virtualization(가상화) 필요
- Utility Computing: on demand, cloud computing
- CPU: socket당 core 여러개가 있음. VM쪽에서 core당 4~5개 가상머신 설치 권장.
  - 2 Socket * 10 Core * 5 VM = 100 VM(s)
- SDN: SW Defined Network
- Network, CPU도 가상화 진행 중
- IT 주도권: 엔지니어 → 프로그래머 → 사용자
- ORDB: Object RDB

## 설치

## Hadoop 명령어

```shell
$ $HADOOP_HOME/bin/hadoop Usage: hadoop [--config confdir] COMMAND where COMMAND is one of:

 namenode -format     format the DFS filesystem
 secondarynamenode    run the DFS secondary namenode
 namenode             run the DFS namenode
 datanode             run a DFS datanode
 dfsadmin             run a DFS admin client
 mradmin              run a Map-Reduce admin client
 fsck                 run a DFS filesystem checking utility
 fs                   run a generic filesystem user client
 balancer             run a cluster balancing utility
 oiv                  apply the offline fsimage viewer to an fsimage
 fetchdt              fetch a delegation token from the NameNode
 jobtracker           run the MapReduce job Tracker node
 pipes                run a Pipes job
 tasktracker          run a MapReduce task Tracker node
 historyserver        run job history servers as a standalone daemon
 job                  manipulate MapReduce jobs
 queue                get information regarding JobQueues
 version              print the version
 jar <jar>            run a jar file
 distcp <srcurl> <desturl> copy file or directories recursively
 distcp2 <srcurl> <desturl> DistCp version 2
 archive -archiveName NAME -p <parent path> <src>* <dest> create a hadoop archive
 classpath            prints the class path needed to get the
                      Hadoop jar and the required libraries
 daemonlog            get/set the log level for each daemon
or
 CLASSNAME            run the class named CLASSNAME
Most commands print help when invoked w/o parameters.
```

### 이것저것 해보기

Java로 map(), reduce()를 구현하여 jar 파일을 돌려야 함. 기본 제공되는 hadoop-examples.jar 이용하여 테스트도 가능.

### 단어 개수 세기

```shell
$ $HADOOP_HOME/bin/hadoop dfs -mkdir input 
$ $HADOOP_HOME/bin/hadoop dfs -put README.txt input/ 
$ $HADOOP_HOME/bin/hadoop jar hadoop-examples-1.2.1.jar wordcount input output
```

## 시험
- 잡이 제출될 때 HDFS에 배포되는 두 개의 파일을 기술하시오
  - job.xml과 job.jar 파일
- 하둡의 네임노드와 보조 네임노드와의 체크포인트 동작을 설명하시오
  - 보조 네임노드: 네임노드에게 에디트 로그 파일을 롤링할 것을 요청
- 재구동할 때 발생하는 블록 리포팅에 대하여 설명
  - 로컬에 저장된 파일 시스템 이미지아 에디트 로그를 조회한 후 메모리에 있는 파일 시스템 이미지를 갱신. 이때 데이터노드는 저장하고 있는 블록의 위치 정보를 네임노드에 전송하고, 네임노드는 메모리에 올라와 있는 파일 시스템 이미지와 데이터노드가 전송한 블록의 정보를 비교하는 작업을 수행. 이러한 비교 작업을 블록 리포팅이라고 하며, 블록 리포팅이 완료되기 전까지의 상태를 안전모드(safemode)라고 함
- 키값을 검색할 수 있게 색인과 데이터가 저장된 파일
  - 맵파일
- MultipleOutput.addNamedOutput()
- 맵퍼가 단독으로 수행하는 조인은?
  - 맵-사이드 조인
- 맵퍼의 출력 데이터가 리듀서에 전달되기 전에 출력 데이터를 줄이는 기능은?
  - 콤바이너
- 하둡에서 자바 외에 맵리듀스 프로그래밍을 가능하게 하는 기능은?
  - 스트리밍
- 하이브 쿼리 중 각 리듀서의 출력이 정렬 되도록 하는 절은?
  - SORT BY
- 하둡 클러스터 환경에서 서버 간 통신에 사용하는 기술은?
  - SSH
- 하둡은 네임스페이스를 동기화하기 위해 체크포인트 매커니즘 사용한다. 기본적으로 1시간인데, 이 체크포인트를 설정하는 속성은?
  - fs.checkpoint.period
- 하둡의 저장 구조를 기초로 하여 구성하는 NoSQL 데이터베이스는?
  - HBase
- 분산 락을 사용하기 위한 모니터링/관리해주는 오픈소스 프로젝트?
  - ZooKeeper
