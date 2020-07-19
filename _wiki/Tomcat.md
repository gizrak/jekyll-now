---
title: Tomcat
category:
  - Web
---

## Tomcat Apache 연계

| OS | mod_jk | proxy_ajp |
|----|--------|-----------|
|Windows|<http://openframework.or.kr/Wiki.jsp?page=Apache_tomcat_using_jk_on_windows>|<http://openframework.or.kr/Wiki.jsp?page=Apache_tomcat_using_modproxy_on_windows>|
|Linux|<http://openframework.or.kr/Wiki.jsp?page=Apache_tomcat_using_jk_on_linux>|<http://openframework.or.kr/Wiki.jsp?page=Apache_tomcat_using_modproxy_on_linux>|

## SSL 인증서 설치
* Tomcat에 SSL 인증서 설치하기 <http://whiteship.me/?p=13548>
* 아파치 httpd에 SSL 인증서 설치하기 <http://whiteship.me/?p=13580>

## WAS heap 메모리 상향 조정
```sh
#export JAVA_HOME=/usr/lib/jvm/java-6-openjdk
export JAVA_HOME=/usr/lib/jvm/jdk1.6.0_26

#export JAVA_OPTS="-Xms512m -Xmx512m -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=10000 -Dcom.sun.management.jmxremote.ssl=false -Dcom.sun.management.jmxremote.authenticate=false -Djava.rmi.server.hostname=70.7.53.200"
export MEM_OPTS="-Xms1024m -Xmx1024m -XX:MaxPermSize=256m -XX:NewSize=768m -XX:MaxNewSize=768m -XX:SurvivorRatio=4 -XX:+UseParallelOldGC -XX:+HeapDumpOnOutOfMemoryError"
#export PROF_OPTS="-agentpath:/home/arch/yjp/libyjpagent.so=port=20000,disablestacktelemetry,disableexceptiontelemetry,builtinprobes=none,delay=10000"
#export GCLOG_OPTS="-verbosegc -Xloggc:/usr/local/tomcat/logs/gclog_$$.log -XX:+PrintGCDetails -XX:+PrintGCTimeStamps"

#export JAVA_OPTS="$MEM_OPTS $PROF_OPTS $GCLOG_OPTS"
export JAVA_OPTS="$MEM_OPTS"
```

## catalina.out 로그 rotate
```
# /etc/logrotate.d/tomcat7
/var/log/tomcat7/catalina.out {
    copytruncate
    daily
    rotate 30
    compress
    missingok
    notifempty
    dateext
}
```
