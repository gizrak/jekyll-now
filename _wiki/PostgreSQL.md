---
title: PostgreSQL
---

## 설치하기
다양한 설치 방법이 가능하다. 공식 홈페이지(<http://www.postgresql.org/download/>)를 방문하면 다양한 OS별로 다양한 설치 옵션이 존재한다.
Mac의 경우 MacPorts로도 가능하지만 그냥 app을 설치하는 것이 편하다.

## 시작하기
psql은 PostgreSQL의 기본 커맨드라인 인터페이스다. 그런데 주의할 것은 PostgreSQL은 root 유저로 구동하지 않고 postgres 유저로 구동해야 한다.

```sh
$ sudo su postgres -c 'psql -h localhost'
```

위의 psql을 실행하기 위해서 환경변수에 PATH를 잡아준다. 설치방법에 따라 경로가 다르겠지만, 만약 Mac에서 app 형식으로 설치했다고 가정할 시 아래와 같다.

```sh
# .bash_profile
PATH ="/Applications/Postgres93.app/Contents/MacOS/bin:$PATH"
```

### 사용자 생성

```sql
CREATE USER jane WITH PASSWORD 'mypassword';
GRANT ALL PRIVILEGES ON DATABASE midnight TO midnight;
```

위에서 생성한 jane 사용자로 mydb에 접속하고자 하는 경우
```sh
$ sudo su postgres -c 'psql -h localhost mydb jane'
```

### 데이터베이스 생성

```sql
CREATE DATABASE [your_database_name];
```

### 데이터베이스 삭제

```sql
DROP DATABASE [your_database_name];
```
