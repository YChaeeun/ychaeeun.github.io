---
title : django 튜토리얼 -1 (설치 & 서버 간단 구동)
date : 2019-07-01
categories:
 - django
---



 

### 더보기

> [1) 장고걸스 튜토리얼](https://tutorial.djangogirls.org/ko/)
>
> [2) 콘다 가상환경 설정하기](https://ychae-leah.tistory.com/77)



## 설치

- 설치하기

  ```shell
  $ pip install django
  ```
  ```shell
  $ python -m django --version
  ```
  - 위 명령어로 버전 확인 할 수 있음

  ```shell
  $ pip install --upgrade django
  ```

  - 최신 버전으로 업그레이드 (기존 버전은 삭제)

- django 웹 서버 설치

  ```shell
  $ django-admin startproject mysite .
  ```

  - 아래와 같은 폴더 구조를 가지게 된다
  - manage.py : 사이트 관리를 도와줌
  - settings.py : 웹사이트 설정
  - urls.py : urlresolver 가 사용하는 패턴 목록 포함

  ![tree]({{site.url}}{{site.baseurl}}/assets/images/dj-1.png)



## 설정변경

- mysite/settings.py 파일 변경하기

  ```shell
  $ vim mysite/settings.py
  ```

- 타임존 변경

  ```python
  TIME_ZONE = 'Asia/Seoul'
  ```

- 정적파일 경로 추가

  ```python
  STATIC_URL = '/static/'
  STATIC_ROOT = os.path.join(BASE_DIR, 'static')
  ```

- 호스트 정보 변경

  - [] 비어있으면 로컬 호스트 주소로만 접근 가능함

  - 만약 웹사이트를 배포하고 싶다면 해당 호스트 정보에 맞게 변경해줘야 한다

  - ex) PythonAnywhere를 통해 배포하고 싶다면

    ```python
    ALLOWED_HOST = ['127.0.0.1', '.pythonanywhere.com']
    ```

- 데이터베이스 변경

  - django는 기본적으로 sqlite3를 제공하고 있다
  
  - 다른 데이터베이스 환경을 사용하고 싶다면 아래 공식 문서에서 관련 내용을 확인할 수 있음
  
    >  [documentation](https://docs.djangoproject.com/en/2.2/ref/databases/)



## 웹 서버 간단 구동!

- 데이터베이스 실행

  ```shell
  $ python manage.py migrate
  ```

- 웹 서버 실행

  ```shell
  $ python manage.py runserver
  ```

![web]({{site.url}}{{site.baseurl}}/assets/images/dj-2.png)

![web]({{site.url}}{{site.baseurl}}/assets/images/dj-3.png)