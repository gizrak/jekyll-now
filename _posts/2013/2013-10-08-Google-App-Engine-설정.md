---
title: "Google App Engine 설정"
categories:
  - 프로그래밍
---

## app.yaml

```yaml
application: cloud-ebook
version: 1
runtime: python
api_version: 1

handlers:
- url: /html
  static_dir: html
  
- url: /js
  static_dir: js
  
- url: /style
  static_dir: style
  
- url: /.*
  script: cloudbook.py
```

## Data Store

## Trouble Shooting

### .pydevproject

아래 GOOGLE_APP_ENGINE 경로가 OS마다 다르게 세팅되어야 한다. 한 플랫폼에서 작성하던 프로젝트를 다른 운영체제에서 정상적으로 가져오기 위해서는 아래 항목을 적절하게 수정해주면 된다.

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?> <?eclipse-pydev version="1.0"?>

<pydev_project> <pydev_property name="org.python.pydev.PYTHON_PROJECT_INTERPRETER">Default</pydev_property> <pydev_property name="org.python.pydev.PYTHON_PROJECT_VERSION">python 2.7</pydev_property> <pydev_variables_property name="org.python.pydev.PROJECT_VARIABLE_SUBSTITUTION"> <key>GOOGLE_APP_ENGINE</key> <value>/Applications/GoogleAppEngineLauncher.app/Contents/Resources/GoogleAppEngine-default.bundle/Contents/Resources/google_appengine</value> </pydev_variables_property> <pydev_pathproperty name="org.python.pydev.PROJECT_SOURCE_PATH"> <path>/cloudbook/src</path> <path>/cloudbook/src</path> </pydev_pathproperty> <pydev_pathproperty name="org.python.pydev.PROJECT_EXTERNAL_SOURCE_PATH"> <path>${GOOGLE_APP_ENGINE}</path> <path>${GOOGLE_APP_ENGINE}/lib/django</path> <path>${GOOGLE_APP_ENGINE}/lib/webob</path> <path>${GOOGLE_APP_ENGINE}/lib/yaml/lib</path> </pydev_pathproperty> </pydev_project>
```

### NotImplementedError: Unable to find the Python PIL library

images.resize 함수를 사용할 때 PIL(Python Image Library)가 없으면 아래와 같이 에러가 발생한다. 이때는 PIL을 설치해줘야 한다.

```
NotImplementedError: Unable to find the Python PIL library. Please view the SDK documentation for details about installing PIL on your system.
```

- Uninstall your PIL
- Download the latest libjpeg from here: http://www.ijg.org/files/jpegsrc.v7.tar.gz
-
        $ tar zxvf jpegsrc.v7.tar.gz
        $ cd jpeg-7
        $ ./configure --enable-shared --enable-static
        $ make
        $ sudo make install
- Download PIL from here: http://effbot.org/downloads/Imaging-1.1.6.tar.gz
- 
        $ tar zxvf Imaging-1.1.6.tar.gz
        $ cd Imaging-1.1.6
- Edit setup.py, set JPEG_ROOT = libinclude("/usr/local")
- Build and setup
        $ python setup.py build
        $ sudo python setup.py install --optimize=1
- Restart eclipse if you are using it. Done!

## References

- 강좌
  - <http://code.google.com/appengine/docs/python/overview.html>
  - <http://code.google.com/appengine/docs/python/gettingstarted/>
- Webapp 레퍼런스
  - <http://code.google.com/appengine/docs/python/tools/webapp/>
- User 레퍼런스
  - <http://code.google.com/appengine/docs/python/users/>
- DataStore 레퍼런스
  - <http://code.google.com/appengine/docs/python/datastore/>
- API 목록
  - <http://appgallery.appspot.com/>
- 템플릿
  - <http://www.djangoproject.com/>
- 샘플코드 다운로드사이트
  - <http://code.google.com/p/google-app-engine-samples/>
- 참고 기타
  - <http://portablepython.com/>
  - <http://www.activestate.com/activepython/downloads>
- Scheduled Tasks With Cron for Python (파이썬 예약작업)
  - <http://code.google.com/appengine/docs/python/config/cron.html>
