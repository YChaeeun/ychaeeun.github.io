---
title : django 정리-1 (기본구조 & runserver 포트, IP변경)
date : 2019-07-03
categories:
 - django
---



> [django document](https://docs.djangoproject.com/ko/2.2/)



## 기본 구조

```shell
tutorial/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        wsgi.py
```



- tutorial/ : 장고 프로젝트와 무관하게 프로젝트를 담는 폴더

- [manage.py](https://docs.djangoproject.com/ko/2.2/ref/django-admin/)
  
  - 장고 프로젝트와 다양한 방법으로 상호작용하는 커맨드라인의 유틸리티 (startproject 할 때 자동으로 만들어 짐)
  - dajngo-admin과 비슷한데, manage.py에는 DJANGO_SETTINGS_MODULE 이라는 게 있어서 해당 장고 프로젝트의 setting.py 값을 알려주는 역할을 함!
  
- mystite/ 
  - 프로젝트를 위한 python 패키지들이 저장되는 폴더
  - 해당 디렉토리의 이름을 이용해서 프로젝트 어디에서나 python패키지를 import 할 수 있다. ex) mysite.url
  
- mysite/`__init__.py`  : 해당 프로젝트를 패키지로 관리하겠다고 알려줌

- mysite/[settings.py](https://docs.djangoproject.com/ko/2.2/topics/settings/) 

  - 현재 장고 프로젝트의 환경 및 구성을 저장 (database, timezone, installed_apps ...)

  - INSTALLED_APPS

    - migration이 실행되면 여기에 작성된 설정들을 탐색해서 필요한 데이터베이스 테이블을 생성해준다

    - django.contrib.admin : 관리용 사이트
    - django.contrib.auth : 인증 시스템
    - django.contrib.contenttype : 컨텐츠 타입을 위한 프레임워크
    - django.contrib.sessions : 세션 프레임워크
    - django.contrib.staticfiles : 정적파일을 관리하는 프레임워크

- mysite/urls.py
  - 현재 장고 프로젝트의 URL 선언을 저장하는 파일
  - 장고로 작성된 사이트의 목차라고도 할 수 있음!
  
- mysite/wsgi.py : 프로젝트를 서비스하기 위한 WSGI 호환 웹 서버의 진입점



### 실행 runserver

- runserver 명령어를 실행하면 기본적으로 내부 IP의 8000번 포트로 개발 서버를 띄움

  ```shell
  $ python manage.py runserver
  ```

- 포트 바꾸기
  ```shell
  $ python manage.py runserver 8080
  ```
  
- 서버 IP 바꾸기

  ```shell
  $ python manage.py runserver 0:8000
  ```

  - 같은 네트워크를 공유하고 있는 다른 컴퓨터에서 접속하고 싶을 때 IP 주소를 0:으로 해주고, settings.py 파일에 ALLOWED_HOST=['*']를 해주면 된다!
  - 각 컴퓨터에 부여된 ip주소를 작성하고, 뒤에 포트까지 붙여주면 접속할 수 있다
  - IP 주소 확인 방법 (윈도우 - ipconfig / 리눅스 - ifconfig)


