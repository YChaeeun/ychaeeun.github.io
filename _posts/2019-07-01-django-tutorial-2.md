---
title : django 튜토리얼 -2 (어플리케이션&모델 생성)
date : 2019-07-01
categories:
 - django
---



### 더보기

> [1) 장고걸스 튜토리얼](https://tutorial.djangogirls.org/ko/)
>
> [2) django 튜토리얼 -1 (설치 & 서버 간단 구동)](https://ychae-leah.tistory.com/131)



## 블로그 어플리케이션 생성하기

- 애플리케이션 생성 (이름은 blog)

  ```shell
  $ python manage.py startapp blog
  ```

- settings.py 에 해당 어플리케이션 추가

  ```shell
  $ vim mysite/settings.py
  ```

  - 파일에 INSTALLED_APPS = [] 부분을 찾아서 맨 마지막에 `'blog',` 를 추가한다

![blog]({{site.url}}{{site.baseurl}}/assets/images/dj-2-1.png)



## 글 모델 만들기

- 모델은 객체(Object)의 한 종류인데, 해당 모델을 저장하면 그 내용이 **데이터베이스에 저장된다.**

  - django의 기본 데이터베이스는 sqlite3 인데, 설정을 통해서 자신이 원하는 데이터베이스로 바꿀 수도 있다

- 모델 필드와 정의하는 방법에 대한 documentations

  > [document-field type](https://docs.djangoproject.com/en/2.0/ref/models/fields/#field-types)

- 지금 만들고자 하는 blog에 Post라는, 블로그 글을 작성하는 객체를 만들어보자

  - 블로그 글에 필요한 속성 : 글쓴이, 제목, 내용, 작성일, 게시일
  - models. -> 해당 내용은 모델이고, 값이 데이터베이스에 저장되어야 함을 의미

  ```python
  from django.db import models
  from django.utils import timezone
  
  
  class Post(models.Model):
      author = models.ForeignKey('auth.User', on_delete=models.CASCADE)
      title = models.CharField(max_length=200)
      text = models.TextField()
      created_date = models.DateTimeField(
              default=timezone.now)
      published_date = models.DateTimeField(
              blank=True, null=True)
  
      def publish(self):
          self.published_date = timezone.now()
          self.save()
  
      def __str__(self):
          return self.title
  ```



## 데이터베이스에 모델을 위한 테이블 만들기

- migrations 확인하기

  ```shell
  $ python manage.py makemigrations blog
  ```

- 데이터베이스에 migrations 모델을 추가

  ```shell
  $ python manage.py migrate blog
  ```

- 매번 모델들을 새로 만들때마다 migration -> migrate를 해줘야 한다

