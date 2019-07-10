---
title : django 튜토리얼2 -1 (앱 생성 & view & urls)
date : 2019-07-05
categories:
 - django
---



> [document 첫 번째 장고 앱 작성하기](https://docs.djangoproject.com/ko/2.2/intro/tutorial01/)



## 설문조사 앱 만들기

- polls 앱 생성하기

  ```shell
  $ python manage.py startapp polls
  ```

  ```shell
  $ tree
  ── polls
      ├── __init__.py
      ├── admin.py
      ├── apps.py
      ├── migrations
      │   └── __init__.py
      ├── models.py
      ├── tests.py
      └── views.py
  ```

  



## views -> urls -> urls 작성하기!

- polls/views.py

  ```python
  from django.http import HttpResponse
  
  def index(request):
      return HttpResponse("Hello! polls index")
  ```

- polls/urls.py

  ```python
  from django.urls import path
  from . import views
  
  urlpatterns =[
      path('', views.index, name='index'),
  ]
  ```

- mystite/urls.py

  ```python
  from django.contrib import admin
  from django.urls import path, include
  
  urlpatterns = [
      path('admin/', admin.site.urls ),
      path('polls/', include('polls.urls')),
  ]
  
  ```



## 실행

- 실행하기

  ```python
  $ python manage.py runserver
  ```

![poll]({{site.url}}{{site.baseurl}}/assets/images/poll-1.png)