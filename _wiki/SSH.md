---
title: SSH
category:
  - Network
---

`Secure SHell`

## Tweak

## 키 생성 및 복사

~~~shell
$ ssh-keygen [root@host ~]# ssh-copy-id node1 
~~~

### .ssh/confg
~~~
$ vim ~/.ssh/config host node1 node1.group node1.group.domain.com
   hostname node1.group.domain.com
   user root
   ForwardX11 yes
$ chmod 0600 ~/.ssh/config 
~~~

### DNS 미사용
~~~
$ vim /etc/ssh/sshd_config useDNS no 
~~~
