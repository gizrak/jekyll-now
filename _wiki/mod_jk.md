---
title: mod_jk
category:
  - Web
---

mod_jk를 사용하면 WAS로 연결되는 요청을 Apache2로 연결할 수가 있게 된다. 이를 통해 정적 리소스를 WAS까지 가지 않고 웹서버에서 직접 처리가 가능하여 성능을 향상시킬 수도 있고, 하나의 웹서버에 다수의 WAS를 구성하여 Load Balancing도 할 수 있다.

## $APACHE_HOME/conf/workers.properties

```properties
workers.tomcat_home=/usr/local/tomcat
workers.java_home=/usr/local/jdk

ps=/

worker.list=trust

worker.trust.port=8009
worker.trust.host=localhost
worker.trust.type=ajp13
worker.trust.lbfactor=1

worker.trust.socket_keepalive=1
worker.trust.socket_timeout=10
```

## $APACHE_HOME/conf/httpd.conf

```conf
# Tomcat 배포 위치로 DocRoot를 변경
DocumentRoot "/usr/local/apache-tomcat-7.0.14/webapps"

# 403 권한 문제를 해결
<Directory />
    Options FollowSymLinks
    AllowOverride None
    Order deny,allow
    #Deny from all
    Allow from all
</Directory>

# mod_jk.so include
LoadModule jk_module modules/mod_jk.so

# mod_jk 기본 설정
<IfModule jk_module>
        JkWorkersFile   conf/workers.properties
        JkShmFile       logs/jk-runtime-status
        JkLogFile       logs/mod_jk.log
        JkLogLevel      warn
        JkLogStampFormat        "[%a %b %d %H:%M:%S %Y]"
</IfModule>

# REST 방식의 URL 이므로 일단 모두 Mount
JkMount /project/*       trust

# 제외하고자 하는 resource 형태만 Unmount
JkUnMount /project/*.manifest    trust
JkUnMount /project/*.htm         trust
JkUnMount /project/*.html        trust
JkUnMount /project/*.js          trust
JkUnMount /project/*.css         trust
JkUnMount /project/*.xml         trust
JkUnMount /project/*.ico         trust
JkUnMount /project/*.txt         trust
JkUnMount /project/font/*        trust
JkUnMount /project/images/*      trust
```

## server.xml
Apache쪽 jk 설정이 모두 끝났으면 이제 Tomcat 쪽에서 AJP 연결을 해주면 된다.

```xml
<!-- Define an AJP 1.3 Connector on port 8009 -->
<Connector port="8009" protocol="AJP/1.3" redirectPort="8443" />
```
