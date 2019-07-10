---
title : django 정리-3 (뷰 view & 장고 url)
date : 2019-07-05
categories:
 - django


---





## 뷰 view

- 조각조각 나뉜 모델과 템플릿들을 연결하는 역할을 하는 것이 뷰view
- 어플리테이션의 "로직"을 만드는 곳으로 모델에서 필요한 정보를 받아와서, 템플릿에 전달하는 역할을 함
  - 모델 : 데이터베이스의 구조
  - 템플릿 : 일정한 형태로 정보들을 보여주기 위해 재사용할 수 있는 파일, 장고의 템플릿 양식은 HTML
- **모델(데이터베이스) --> 뷰 --> 템플릿(HTML)**



### 예를 들어서

  ```python
#blog/views.py
from django.shortcuts import render
from django.utils import timezone
from .models import Post
  
def post_list(request):
    posts = Post.objects.filter(published_date__lte=timezone.now()).order_by('published_date')
      return render(request, 'blog/post_list.html', {'posts':posts})
  ```

- request : 사용자가 요청하는 모든 것
- posts : ORM 쿼리셋으로 Post 글들을 데이터베이스에서 가져와서 저장
- return render(... , **{'posts':posts}**) : 위 posts에 담긴 정보들을 posts 라는 매개변수에 담아서 blog/post_list.html 템플릿에 전달





## url

- 장고는 URLconf (URL configurations) 를 사용해서 URL과 일치하는 뷰를 찾아서 사용자에게 정보를 보여줌

- 만약 mysite라는 최상위 폴더 아래에 blog라는 어플리케이션이 있는 구조라면 뷰와 url 파일은 다음과 같은 관계를 가진다

  - blog/views.py에서 blog의 모델과 템플릿을 연결 --> blog/urls.py 에서 blog/views.py의 url을 등록 --> 최상위 URLconf인 mysite/urls.py에 **include()** 함수를 이용해 blog.urls 전체를 등록한다.
  - **blog/views.py (models & templates) --> blog/urls.py --> mysite/urls.py**

- blog/urls.py

  ```python
  from django.urls import path
  from . import views
  
  urlpatters = [
      path('', views.post_list, name='post_list'),  
      # views에서 정의한 def post_list()
  ]
  ```

- mysite/urls.py

  ```python
  from django.contrib import admin
  from django.urls import path, include
  
  urlpatterns = [
      path('admin/', admin.site.urls),
      path('blog/<int:num>/', include('blog.urls'))
  ]
  ```

  - include()
    - 다른 URLconf를 참조할 수 있게 도와주는 함수
    - admin.site.urls 를 제외한 그외 다른 URL 패턴을 포함할 때마다 항상 include를 사용해야 한다!
  - path() 
    - path함수에는 필수 인자인 route와 view & 선택 인자인 kwargs와 name 을 받는다
    - route :  url 패턴을 가진 문자열 / 요청된 패턴을 찾기 위해 각 패턴과 리스트를 순서대로 비교함 / `<int:num> `처럼  변수를 view로 전달 할 수도 있다
    - view : 장고에서 일치하는 url 패턴을 찾으면  특정한 view 함수를 호출한다
    - kwargs : view에 딕셔너리 형태로 전달되는 임의의 키워드들
    - name : 템플릿을 포함한 장고 어디에서나 정확하게 참조할 수 있도록 고유한 이름을 붙여줄 수 있다 / 이 이름은 뷰의 이름과는 상관없이 지어도 됨