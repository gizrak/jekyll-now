---
title: NodeJS 기반의 stg prd 환경구축
categories:
  - 프로그래밍
---

* NodeJS 기반으로 mysvc라는 이름의 서비스를 하나 구축한다.
* 운영체제는 Linux, 웹서버는 Nginx, 저장소는 Git을 사용한다.

## STG 환경

1. 소스코드가 이미 있다고 가정하고 stg 디렉토리로 코드 pull

```sh
$ mkdir -p ~/stg
$ cd ~/stg
$ git checkout ssh://mysvc@localhost:~/mysvc.git
```

2. STG 구동을 위한 서비스 등록

```sh
####/bin/sh

NODE_ENV="development"
PORT="3000"
APP_DIR="~mysvc/stg"
NODE_APP="server.js"
CONFIG_DIR="$APP_DIR"
PID_FILE="/var/run/mysvc_stg.pid"
LOG_DIR="/var/log/mysvc"
LOG_FILE="$LOG_DIR/stg.log"
NODE_EXEC=$(which node)

###############

1. REDHAT chkconfig header

1. chkconfig: - 58 74
1. description: node-app is the script for starting a node app on boot.
## BEGIN INIT INFO
1. Provides: node
1. Required-Start:    $network $remote_fs $local_fs
1. Required-Stop:     $network $remote_fs $local_fs
1. Default-Start:     2 3 4 5
1. Default-Stop:      0 1 6
1. Short-Description: start and stop node
1. Description: Node process for app
## END INIT INFO

###############

USAGE="Usage: $0 {start|stop|restart|status} [--force]"
FORCE_OP=true

pid_file_exists() {
    [ -f "$PID_FILE" ]
}

get_pid() {
    echo "$(cat "$PID_FILE")"
}

is_running() {
    PID=$(get_pid)
    ### [ -z "$(ps aux | awk '{print $2}' | grep "^$PID$")" ]
}

start_it() {
    mkdir -p "$LOG_DIR"

    echo "Starting node app ..."
    PORT="$PORT" NODE_ENV="$NODE_ENV" NODE_CONFIG_DIR="$CONFIG_DIR" $NODE_EXEC "$APP_DIR/$NODE_APP"  1>"$LOG_FILE" 2>&1 &
    echo $### > "$PID_FILE"
    echo "Node app started with pid $###"
}

stop_process() {
    PID=$(get_pid)
    echo "Killing process $PID"
    kill $PID
}

remove_pid_file() {
    echo "Removing pid file"
    rm -f "$PID_FILE"
}

start_app() {
    if pid_file_exists
    then
        if is_running
        then
            PID=$(get_pid)
            echo "Node app already running with pid $PID"
            exit 1
        else
            echo "Node app stopped, but pid file exists"
            if [ $FORCE_OP = true ]
            then
                echo "Forcing start anyways"
                remove_pid_file
                start_it
            fi
        fi
    else
        start_it
    fi
}

stop_app() {
    if pid_file_exists
    then
        if is_running
        then
            echo "Stopping node app ..."
            stop_process
            remove_pid_file
            echo "Node app stopped"
        else
            echo "Node app already stopped, but pid file exists"
            if [ $FORCE_OP = true ]
            then
                echo "Forcing stop anyways ..."
                remove_pid_file
                echo "Node app stopped"
            else
                exit 1
            fi
        fi
    else
        echo "Node app already stopped, pid file does not exist"
        exit 1
    fi
}

status_app() {
    if pid_file_exists
    then
        if is_running
        then
            PID=$(get_pid)
            echo "Node app running with pid $PID"
        else
            echo "Node app stopped, but pid file exists"
        fi
    else
        echo "Node app stopped"
    fi
}

case "$2" in
    --force)
        FORCE_OP=true
    ;;

    "")
    ;;

    *)
        echo $USAGE
        exit 1
    ;;
esac

case "$1" in
    start)
        start_app
    ;;

    stop)
        stop_app
    ;;

    restart)
        stop_app
        start_app
    ;;

    status)
        status_app
    ;;

    *)
        echo $USAGE
        exit 1
    ;;
esac
```

## PRD 환경

1. prd 디렉토리 생성 및 stg 환경 복사

```sh
$ mkdir -p ~/prd
$ cd ~/prd
$ git clone ssh://mysvc@localhost:~/stg
```

2. 서비스 스크립트 /etc/init.d/prd 작성

```sh
####/bin/sh

NODE_ENV="production"
PORT="5000"
APP_DIR="~mysvc/prd"
NODE_APP="server.js"
CONFIG_DIR="$APP_DIR"
PID_FILE="/var/run/mysvc_prd.pid"
LOG_DIR="/var/log/mysvc"
LOG_FILE="$LOG_DIR/prd.log"
NODE_EXEC=$(which node)

###############

1. REDHAT chkconfig header

1. chkconfig: - 58 74
1. description: node-app is the script for starting a node app on boot.
## BEGIN INIT INFO
1. Provides: node
1. Required-Start:    $network $remote_fs $local_fs
1. Required-Stop:     $network $remote_fs $local_fs
1. Default-Start:     2 3 4 5
1. Default-Stop:      0 1 6
1. Short-Description: start and stop node
1. Description: Node process for app
## END INIT INFO

###############

USAGE="Usage: $0 {start|stop|restart|status} [--force]"
FORCE_OP=true

pid_file_exists() {
    [ -f "$PID_FILE" ]
}

get_pid() {
    echo "$(cat "$PID_FILE")"
}

is_running() {
    PID=$(get_pid)
    ### [ -z "$(ps aux | awk '{print $2}' | grep "^$PID$")" ]
}

start_it() {
    mkdir -p "$LOG_DIR"

    echo "Starting node app ..."
    PORT="$PORT" NODE_ENV="$NODE_ENV" NODE_CONFIG_DIR="$CONFIG_DIR" $NODE_EXEC "$APP_DIR/$NODE_APP"  1>"$LOG_FILE" 2>&1 &
    echo $### > "$PID_FILE"
    echo "Node app started with pid $###"
}

stop_process() {
    PID=$(get_pid)
    echo "Killing process $PID"
    kill $PID
}

remove_pid_file() {
    echo "Removing pid file"
    rm -f "$PID_FILE"
}

start_app() {
    if pid_file_exists
    then
        if is_running
        then
            PID=$(get_pid)
            echo "Node app already running with pid $PID"
            exit 1
        else
            echo "Node app stopped, but pid file exists"
            if [ $FORCE_OP = true ]
            then
                echo "Forcing start anyways"
                remove_pid_file
                start_it
            fi
        fi
    else
        start_it
    fi
}

stop_app() {
    if pid_file_exists
    then
        if is_running
        then
            echo "Stopping node app ..."
            stop_process
            remove_pid_file
            echo "Node app stopped"
        else
            echo "Node app already stopped, but pid file exists"
            if [ $FORCE_OP = true ]
            then
                echo "Forcing stop anyways ..."
                remove_pid_file
                echo "Node app stopped"
            else
                exit 1
            fi
        fi
    else
        echo "Node app already stopped, pid file does not exist"
        exit 1
    fi
}

status_app() {
    if pid_file_exists
    then
        if is_running
        then
            PID=$(get_pid)
            echo "Node app running with pid $PID"
        else
            echo "Node app stopped, but pid file exists"
        fi
    else
        echo "Node app stopped"
    fi
}

case "$2" in
    --force)
        FORCE_OP=true
    ;;

    "")
    ;;

    *)
        echo $USAGE
        exit 1
    ;;
esac

case "$1" in
    start)
        start_app
    ;;

    stop)
        stop_app
    ;;

    restart)
        stop_app
        start_app
    ;;

    status)
        status_app
    ;;

    *)
        echo $USAGE
        exit 1
    ;;
esac
```

3. stg의 코드를 prd로 merge하고 배포하기 위한 스크립트 작성

```sh
####/bin/sh

cd ~/prd
git pull localhost:~/stg
npm install
service prd restart
```

## Nginx 설정

1. stg, prd에 대한 reverse proxy 설정

```nginx
server {
        ...
        location / {
        }

        location /mysvc {
            proxy_pass http://localhost:5000/mysvc;
            proxy_set_header X-Forwarded-For $remote_addr;
            proxy_set_header Host $host;
        }

        location /mysvc_stg {
            proxy_pass http://localhost:3000/mysvc_stg;
            proxy_set_header X-Forwarded-For $remote_addr;
            proxy_set_header Host $host;
        }
        ...
}
```

2. 서비스 재구동

```sh
$ sudo service stg restart
$ sudo service prd restart
```
