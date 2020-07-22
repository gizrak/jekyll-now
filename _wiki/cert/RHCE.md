---
title: RHCE
category:
  - 자격증
---

`Red Hat Certified Engineer`

- RedHat 리눅스 시스템 관리, 네트워크, 보안에 대한 전문지식을 보유하고 있음을 인증
- 리눅스 전문지식에 대한 자격증으로는 LPIC[^1]가 있음

## 예상 문제

### selinux 활성화

### ip forwarding 설정

~~~
/etc/sysctl.conf
~~~

### cron 설정

~~~
/etc/cron.deny
~~~

### anonymous ftp

### samba

1. 설치
    ~~~shell
    $ yum install -y samba
    ~~~
1. samba 전용 그룹 생성 및 사용자 설정 
    ~~~shell
    $ groupadd project useradd -aG project guru
    ~~~
1. 디렉토리 생성 및 권한 설정
    ~~~shell
    $ mkdir /project 
    $ chgrp project /project 
    $ chmod 2770 /project
    ~~~
1. selinux 설정
    ~~~shell
    $ selinux chcon -R -t samba_share_t /project getsebool -a | grep samba; setsebool -P samba_enable_home_dirs on
    ~~~
1. 설정 파일 수정(데몬 재가동 & 부팅시 설정 포함) 
    ~~~properties
    # /etc/samba/smb.conf
    workgroup = HPEDU hosts allow = x.x.x. ; or 방화벽 설정
    
    [project] ; 기존 설정 복사 comment = hp-project path = /project writable = yes (browsable = yes) write list = +project ; or guru
    ~~~
1. 재구동
    ~~~shell
    $ service smb restart 
    $ chkconfig smb on
    ~~~
1. 방화벽 설정 
    ~~~shell
    $ system-config-firewall → smb 선택
    ~~~
1. samba 계정 설정 
    ~~~shell
    $ smbpasswd -a guru
    ~~~
1. test 
    ~~~shell
    $ smbclient -L //IP -U guru 
    $ mount -t cifs -o user=gure //IP/project /mnt 
    $ df -h
    ~~~

### nfs

1. 설치
    ~~~shell
    $ yum install -y nfs-utils 
    ~~~
1. 설정
    ~~~conf
    # /etc/exports
    /common IP(ro,sync) 
    ~~~
1. 재구동
    ~~~shell
    $ service nfs restart 
    $ chkconfig nfs on 
    ~~~
1. 방화벽
    ~~~shell
    $ system-config-firewall → NFS4 선택
    ~~~

### postfix

1. 설치
    ~~~shell
    $ yum install -y postfix 
    ~~~
1. 설정
    ~~~conf
    # /etc/postfix/main.cf (or postconf -e "inet_interfaces = all")
    inet_interfaces = all
    
    inet_interfaces = localhost
    ~~~
1. 재구동
    ~~~shell
    $ service postfix restart 
    $ chkconfig postfix on 
    ~~~
1. 방화벽
    ~~~shell
    $ system-config-firewall → Mail (SMTP) 선택 
    ~~~
1. ailas 설정
    ~~~properties
    # /etc/aliases
    guru: visitor
    ~~~
1. alias 적용
    ~~~shell
    $ newaliases 
    ~~~
1. test (다른 시스템)
    ~~~shell
    $ mailx guru@192.168.56.201 $ mailq 
    ~~~

### httpd

1. 설치 및 설정 (데몬 재가동 & 부팅시 설정 포함)
  - [Apache](/wiki/Apache) 항목 참조
1. selinux
    ~~~shell
    $ ls -ldZ /var/www/html 
    $ chcon -R -t httpd_sys_content_t /www 
    $ ls -ldZ /www 
    ~~~
1. 방화벽
    ~~~
    $ system-config-firewall → WWW(HTTP) 선택 
    ~~~
1. httpd 디렉토리 접근 설정
    ~~~apache
    <Directory "/var/www/virtual/security">
    
       Options Indexes FollowSymLinks
       AllowOverride None
       Order allow,deny
       Allow from IP  ### 이 부분이 중요
    </Directory> 
    ~~~

### httpd 가상 호스트

1. 설정 (데몬 재가동 & 부팅시 설정 포함)
    ~~~apache
    # /etc/httpd/conf/httpd.conf
   
    NameVirtualHost *:80
    
    <VirtualHost *:80>
    
    ServerAdmin webmaster@dummy-host.example.com
       DocumentRoot /www
       ServerName server.example.com
    ErrorLog logs/dummy-host.example.com-error_log
    CustomLog logs/dummy-host.example.com-access_log common
    </VirtualHost>
    
    <VirtualHost *:80>
    
    ServerAdmin webmaster@dummy-host.example.com
       DocumentRoot /var/www/virtual
       ServerName www.example.com
    ErrorLog logs/dummy-host.example.com-error_log
    CustomLog logs/dummy-host.example.com-access_log common
    </VirtualHost> 
    ~~~
1. 재구동
    ~~~shell
    $ service httpd restart 
    $ chkconfig httpd on 
    ~~~
1. 디렉토리 생성 및 파일 다운 로드
    ~~~shell
    $ mkdir /var/www/virtual 
    $ wget ftp://my.site.com/virtualpage.html 
    $ mv virtualpage.html index.html 
    ~~~
1. selinux
    ~~~shell
    $ ls -lZ /var/www/virtual 
    ~~~
1. test
    ~~~shell
    $ lynx http://server201.example.com 
    $ lynx http://www201.example.com 
    ~~~

### iscsi

1. 설치 및 start(enable)
    ~~~shell
    $ yum install -y iscsi-initiator-utils 
    $ service iscsid start $ chkconfig iscsid on 
    ~~~
1. iscsi 서버 질의 및 로그인
    ~~~shell
    $ iscsiadm -m discovery -t st -p {iSCSI Server IP}
    $ iscsiadm -m node -T iqn~~ -p {iSCSI Server IP} -l 
    $ iscsiadm -m node -T iqn~~ -p {iSCSI Server IP} -o update -n node.startup -v automatic
    $ dmesg | tail
    ~~~
1. disk 작업
    ~~~shell
    $ fdisk -cu /dev/sde 
    $ mkfs -t ext4 /dev/sde1 
    $ mkdir /iscsi $ vi /etc/fstab 
    $ mount /iscsi
    ~~~

### ssh 접근제어

### 스크립트 작성

### 부팅시 커널값 설정

아래 파일을 편집하여 kernel 제일 뒤쪽에 원하는 값을 세팅하여 넣음
    ~~~shell
    $ vi /boot/grub/grub.conf
    ~~~

### iso mount

    ~~~properties
    iso9660 ro,loop
    ~~~

## 추가 예상 문제

### httpd 인증 설정 (File)

1. 디렉토리 생성 및 파일 다운로드
    ~~~shell
    $ cd /var/www/virtual 
    $ mkdir security 
    $ wget ftp://my.site.com/security.html
    ~~~
1. 인증
    ~~~shell
    $ htpasswd -c -m /var/www/.userlist guru
    ~~~
1. 설정(데몬 재가동 & 부팅시 설정 포함)
    ~~~apache
    # /etc/httpd/conf/httpd.conf
    
    <VirtualHost *:80>

    ServerAdmin webmaster@dummy-host.example.com
       DocumentRoot /var/www/virtual
       ServerName www201.example.com
           <Directory "/var/www/virtual/security">
               Options Indexes FollowSymLinks
               AllowOverride None
                   AuthName "Security"
                   AuthType basic
                   AuthUserFile "/var/www/.userlist"
                   Require vaild-user
               Order allow,deny
               Allow from all
           </Directory>
    ErrorLog logs/dummy-host.example.com-error_log
    CustomLog logs/dummy-host.example.com-access_log common
    </VirtualHost>
    ~~~
1. 재구동
    ~~~shell
    $ service httpd restart
    $ chkconfig httpd on
    ~~~
1. 검증
    ~~~shell
    $ lynx http://IP/security/security.html
    ~~~

### httpd 인증설정(LDAP)

1. 디렉토리 생성 및 파일 다운로드 
    ~~~shell
    $ cd /var/www/virtual
    $ mkdir security
    $ wget ftp://my.site.com/security.html 
    ~~~
1. 인증서 파일 설치 
    ~~~shell
    $ cd /etc/httpd
    $ wget http://my.site.com/server.crt 
    ~~~
1. 설정(데몬 재가동 & 부팅시 설정 포함) 
    ~~~apache
    # /etc/httpd/conf/httpd.conf
    
    LDAPTrustedGlobalCert CA_BASE64 /etc/httpd/server.crt <VirtualHost *:80>
    
    ServerAdmin webmaster@dummy-host.example.com
       DocumentRoot /var/www/virtual
       ServerName www201.example.com
           <Directory "/var/www/virtual/security">
               Options Indexes FollowSymLinks
               AllowOverride None
                   AuthName "Security"
                   AuthType basic
                    AuthBasicProvider ldap <<<<<
                   AuthLDAPUrl "ldap://xxx/dc=example,dc=com" TLS
                   Require vaild-user
               Order allow,deny
               Allow from all
           </Directory>
    ErrorLog logs/dummy-host.example.com-error_log
    CustomLog logs/dummy-host.example.com-access_log common
    </VirtualHost> 
    ~~~
1. 재구동 
    ~~~shell
    $ service httpd restart 
    $ chkconfig httpd on 
    ~~~

### caching name server

1. 설치
~~~shell
$ yum install -y bind
~~~
2. 설정
~~~conf
/etc/named.conf
listen-on port 53 { any; }; 
listen-on-v6 port 53 { any; }; 
allow-query { localhost; 192.168.56.0/24; }; 
forwarders { 192.168.56.201; }; 
dnssec-validation no;

(rndc-confgen -a) service named restart chkconfig named on
~~~

### log 서버

1. 설정 (클라이언트)
    ~~~shell
    /etc/rsyslog.conf
    .info @rhce
    ~~~
1. 설정 (서버)
    ~~~shell
    /etc/rsyslog.conf
    Provides UDP syslog reception
    $ModLoad imudp $UDPServerRun 514
    
    Provides TCP syslog reception
    $ModLoad imtcp $InputTCPServerRun 514
    ~~~
1. 재구동
    ~~~shell
    $ service rsyslogd restart
    ~~~
1. 방화벽 설정
    ~~~shell
    $ service iptables save
    $ vi /etc/sysconfig/iptables
    $ iptables -A INPUT -p tcp -m state --state NEW -m tcp --dport 514 -j ACCEPT 
    $ iptables -A INPUT -p udp -m state --state NEW -m udp --dport 514 -j ACCEPT 
    $ service iptables restart $ iptables -L
    ~~~
1. 테스트
    ~~~shell
    $ tail /var/log/messages
    ~~~

[^1]: Linux Professional Instritute Certified
