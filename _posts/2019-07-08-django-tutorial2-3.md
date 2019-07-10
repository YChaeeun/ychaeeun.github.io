---
title : django 튜토리얼2 -3 (관리자admin 사이트 생성)
date : 2019-07-08
categories:
 - django


---



> [document 첫 번째 장고 앱 작성하기](https://docs.djangoproject.com/ko/2.2/intro/tutorial02/)



## 관리자 생성하기(슈퍼유저)

- 슈퍼유저 생성하기

  ```shell
  $ python manage.py createsuperuser
  ```

  - username과 email address를 입력해주면 끝!

- 서버를 실행하고, 포트뒤에 /admin 을 입력하면 관리자 사이트 로그인 화면이 뜬다 (http://127.0.0.1:8000/admin)

![admin]({{stie.url}}{{site.baseurl}}/assets/images/admin-1.png)

- 로그인을 하면 편집가능한 그룹, 사용자 정보 같은 컨텐츠를 볼 수 있는데, **django.contrib.auth** 라는 인증 프레임워크 모듈이 있기 때문에 가능!



## 관리 사이트에 앱 등록하기

- 만든 Question과 Choice라는 앱 중에 Question도 관리 인터페이스를 가질 수 있도록 앱 등록하기

- polls/admin.py

  ```python
  from django.contrib import admin
  from .models import Question
  
  admin.site.register(Question)
  ```

  

## 관리페이지 수정하기

![admin]({{site.url}}{{site.baseurl}}/assets/images/admin-2.png)



- 위 서식은 Question 모델에서 자동으로 생성된 서식!
- 기본 옵션으로는 저장(Save) / 저장 및 편집 계속(Save and continue editing) / 저장 및 다른 이름으로 추가(Save and add another) / 삭제(Delete)
- HISTORY 를 통해서 과거 기록도 살펴볼 수 있음