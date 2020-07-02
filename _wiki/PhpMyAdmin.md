---
title: PhpMyAdmin
---

## 로그인 시간 연장
/etc/config.inc.php 파일 수정

```php
$cfg['LoginCookieValidity'] = 3600 * 9; // 9 hours
```

## 업로드 파일 사이즈
/etc/php5/apache2/php.ini 파일 수정

```
upload_max_filesize = 64M
```
