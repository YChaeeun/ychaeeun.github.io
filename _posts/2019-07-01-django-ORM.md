---
title : django ORM 정리
date : 2019-07-01
categories:
 - django
---



## 장고 shell 열고 import

- 장고 인터랙티브 콘솔 (interactive console)

  ```shell
  $ python manage.py shell
  ```

- 자신이 다루고 싶은 객체를 import해와야 함

  ```shell
  >>> from blog.models import Post
  >>> from django.contrib.auth.models import User
  ```

  - 이전에 정의했던 blog 모델의 Post 객체를 import 해옴
  - User 사용자 정보도 import

- 장고 shell을 종료하고 싶을 때는 exit() 입력하면 끝!



## 데이터 가져오기 objects.all() & get()

- 데이터 조회

  ```shell
  >>> Post.objects.all()
  <QuerySet [<Post: one>, <Post: two>]>
  ```

  - Post의 모델의 게시된 글 목록을 조회할 수 있음

  ```shell
  >>> User.objects.all()
  <QuerySet [<User:ychaen>]
  ```

  - 이전에 설정했던 superuser를 조회

- 데이터 가져오기

  ```shell
  >>> me = User.objects.get(username='ychae')
  ```

  - 사용자의 인스턴스(instance)를 가져와서 me에 저장



## 데이터 추가하기 objects.create()

- Post 객체에 글 추가하기

  ```shell
  >>> Post.objects.create(author=me, title='three', text='third text')
  ```

- User 객체에 사용자 추가하기

  ```shell
  >>> User.objects.create(username='user2')
  ```

- 추가한 내용을 확인하려면 데이터를 조회해보면 됨

  ```shell
  >>> Post.objects.all()
  <QuerySet [<Post: one>, <Post: two>, <Post: three>]>
  ```

- 방금 작성한 글을 바로 게시하고 싶다면 Post 객체에 정의한 함수 publish()를 사용하면 된다.

  ```shell
  >>> post = Post.objects.get(title='three')
  >>> post.publish()
  ```

  - 우선 인스턴스를 받아온 뒤에, publish() 메서드 사용



## 검색 objects.filter()

- 만약 ychaen이 작성한 글만 보고 싶다면, filter()를 사용해서 원하는 글들만 가져올 수 있다

  ```shell
  >>> me = User.objects.get(username='ychaen')
  >>> Post.objects.filter(author=me)
  <QuerySet [<Post: one>, <Post: two>, <Post: three>]>
  ```

- 만약 title에 two 라는 글자가 들어간 글들만 뽑아내고 싶다면?

  ```shell
  >>> Post.objects.filter(title__contains='two')
  <QuerySet [<Post: two>]>
  ```

  - 던더스코어로 작성해야 함! (언더스코어 두개 __)



## 정렬하기 objects.order_by()

- create_date를 기준으로 오름차순 정렬

  ```shell
  >>> Post.objects.order_by('created_date')
  ```

- 내림차순 정렬 (앞에 - 마이너스 붙이기)

  ```shell
  >>> Post.objdects.order_by('-created_date')
  ```

  



## 쿼리셋 연결하기

- 위의 기능들을 여러 개 적어주면 복잡한 쿼리도 쉽게 작성할 수 있게 됨!!

- ychaen 이라는 유저가 작성한 글들을 published_date를 기준으로 오름차순 정렬한다면?

  ```shell
  >>> me = User.objects.get(username='ychaen')
  >>> Post.objects.filter(author=me).order_by('published_date')
  ```

  