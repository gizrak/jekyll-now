---
title: MySQL
---

* MySQL 데이터타입: <http://ra2kstar.tistory.com/82>
* MySQL 사용자: <http://gpgstudy.com/gpgiki/MySQL에서%20사용자와%20데이터베이스%20만들기>

## DDL

### 테이블 생성

```sql
CREATE TABLE TABLE_NAME (
    id INT(5) UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50) DEFAULT '-' NOT NULL,
    age INT,
    address longtext,
    birthday DATE
);
```

### 인덱스 생성

```sql
CREATE [UNIQUE] INDEX index_name ON tbl_name (col_name[(LENGTH]),... )
```

### 인덱스 삭제

```sql
DROP INDEX index_name;
```

## DML

### 테이블에 새로운 컬럼 추가

```sql
ALTER TABLE tablename ADD COLUMN [추가할 컬럼명] [추가할 컬럼 데이타형]
```

### 테이블에 컬럼타입 변경하기

```sql
ALTER TABLE tablename MODIFY COLUMN [변경할 컬럼명] [변경할 컬럼 타입]
```

### 테이블에 컬럼이름 변경하기

```sql
ALTER TABLE tablename CHANGE COLUMN [기존 컬럼명] [변경할 컬럼명] [변경할 컬럼타입]
```

### 테이블에 컬럼 삭제하기

```sql
ALTER TABLE tablename DROP COLUMN [삭제할 컬럼명]
```

### 테이블컬럼에 인덱스 주기

```sql
ALTER TABLE tablename ADD INDEX 인덱스명(인덱스를 줄 컬럼1 , 인덱스를 줄 컬럼2, ... )
```

### 테이블컬럼에 인덱스 삭제하기

```sql
ALTER TABLE tablename DROP INDEX 인덱스명;
```

### 테이블에 Primary Key 만들기

```sql
ALTER TABLE tablename ADD PRIMARY KEY (키를 줄 컬럼명1 , 키를 줄 컬럼명2, ...)
```

### 테이블에 Primary Key 삭제하기

```sql
ALTER TABLE tablename DROP PRIMARY KEY;
```

### 테이블명 바꾸기

```sql
ALTER TABLE 기존테이블명 RENAME 새로운테이블명
```

## 시스템

### 발생한 오류나 경고 다시 보기

```
sql> SHOW errors;
Empty SET (0.00 sec)

sql> SHOW warnings;
Empty SET (0.00 sec)
```

### 현재 상태 보기

```
sql> STATUS
--------------
sql  Ver 14.14 Distrib 5.5.31, FOR debian-linux-gnu (x86_64) USING readline 6.2

Connection id:          18579
CURRENT DATABASE:       postblog
CURRENT USER:           root@localhost
SSL:                    NOT IN USE
CURRENT pager:          stdout
USING OUTFILE:          ''
USING delimiter:        ;
Server version:         5.5.31-0ubuntu0.12.04.1 (Ubuntu)
Protocol version:       10
Connection:             Localhost via UNIX socket
Server characterset:    utf8
Db     characterset:    utf8
Client characterset:    utf8
Conn.  characterset:    utf8
UNIX socket:            /var/run/sqld/sqld.sock
Uptime:                 7 days 23 hours 15 MIN 6 sec

Threads: 50  Questions: 1119179  Slow queries: 0  Opens: 6613  FLUSH TABLES: 1  OPEN TABLES: 400  Queries per SECOND avg: 1.625
--------------
```

## 간단한 설정

```
thread_cache_size       = 16384 # default는 8
sort_buffer_size        = 8M    # default는 2M
tx_isolation            = READ-COMMITTED # REPEATABLE-READ, READ-UNCOMMITTED
innodb_buffer_pool_size = 7G
```

MySQL에서 현재 설정되어 있는 환경변수를 보기 위해서는 아래와 같이 쿼리
```sql
show variables where variable_name like 'thread%';
```

MySQL에서 현재 구동하고 있는 쿼리 프로세스들을 보기 위해선 아래와 같이 쿼리
```sql
show full processlist;
```

## root 암호 변경

### secure installation
```sh
$ mysql_secure_installation
```

### mysqladmin을 이용
```sh
$ mysqladmin -u root password new-password
```

### update문을 이용
```sql
UPDATE USER SET password = password('new-password') WHERE USER = 'root';
FLUSH privileges;
```

### set password를 이용
```sql
SET password FOR root = password('new-password');
```
