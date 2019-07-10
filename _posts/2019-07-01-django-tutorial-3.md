---
title : django 튜토리얼 -3 (admin & super user 생성)
date : 2019-07-01
categories:
 - django

---



### 더보기

> [1) 장고걸스 튜토리얼](https://tutorial.djangogirls.org/ko/)
>
> [2) django 튜토리얼 -1 (설치 & 서버 간단 구동)](https://ychae-leah.tistory.com/131)
>
> [3) djago 튜토리얼 -2 (어플리케이션&모델 생성)]()





## ADMIN 관리자 페이지

- settings.py 의 LANGUAGE_CODE 를 'ko' 로 바꾸면 한국어 관리자 화면을 설정할 수 있음

- 슈퍼 사용자 생성하기 superuser

  ```shell
  $ python manage.py createsuperuser
  ```

  - 소문자로 공백없이 이름과 메일, 암호를 입력해줌

- 관리자 페이지에 블로그 모델 등록하기

  ```shell
  $ vim blog/admin.py
  ```

  ```python
  from django.contrib import admin
  from .models import Post
  
  admin.site.register(Post)
  ```

- `python manage.py runserver` 로 웹서버를 실행하고 127.0.0.1/admin 으로 접속

- 블로그 모델을 등록하고, superuser로 로그인 하면 아래와 같은 화면이 뜬다

![admin]({{site.url}}{{site.baseurl}}/assets/images/dj-2-2.png)

- 글 작성하기

![admin]({{site.url}}{{site.baseurl}}/assets/images/dj-2-3.png)