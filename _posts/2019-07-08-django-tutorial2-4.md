---
title : django 튜토리얼2 -4 (뷰 view & 템플릿)
date : 2019-07-08
categories:
 - django



---



> [document 첫 번째 장고 앱 작성하기](https://docs.djangoproject.com/ko/2.2/intro/tutorial03/)

> [장고 정리 - 뷰 view & url](https://ychae-leah.tistory.com/140)



## 뷰 view

- 뷰view는 어플리케이션의 "로직"을 만드는 곳! 파이썬의 어떠한 라이브러리라도 사용할 수 있다
- 모델에서 필요한 정보를 받아와서, 로직을 구현하고, 템플릿으로 전달하는 역할을 한다
- 장고는 요청된 url을 조사해서, 위에서부터 view를 탐색함
  - 예쁜(?) url을 위해서 장고에는 URLconfs 라는 것을 사용
  - ex) URL 패턴 : `/article/new/<year>/<month>`
- polls 어플리케이션에 필요한 기능들을 아래와 같이 정의하고 각각 view를 작성해 줄 예정
  - 질문 색인 페이지 index - 최근 질문들을 표시
  - 질문 세부 페이지 detail - 질문 내용과 투표할 수 있는 서식을 표시
  - 질문 결과 페이지 result - 특정 질문에 대한 결과 표시
  - 투표 기능 vote - 특정 질문에 대해 특정 선택을 할 수 있는 투표 기능을 제공





## 뷰 : url에서 정보 받아오기

- 인수를 받아오는 뷰

- polls/views.py

  ```python
  def detail(request, question_id):
  	return HttpResponse("question list %s" %question_id)
  
  def result(request, question_id):
      response = "result : %s"
      return HttpResponse(response % question_id)
  
  def vote(request, question_id):
      return HttpResponse("vote for %s" %question_id)
  ```
  - 이때 "  ",  % 콤마 찍으면 안 돼
  - 파이썬이니까 f"question list {question_id} 형식으로 작성해도 됨!

- 해당 뷰에 필요한 인수인 question_id 를 url로 받아오기 위해서는 urls.py를 수정해야 함

  ```python
  from django.urls import path
  
  from . import views
  
  urlpatterns = [
      path('', views.index, name="index"),
      path('<int:question_id>/', views.detail, name="detail"),
      path('<int:question_id>/results/', views.result, name="result"),
      path('<int:question_id>/vote/', views.vote, name="vote"),
  ]
  ```

  - 뒤에 꼬박꼬박 `/` 붙이기!
  - 이전에 mysite/urls.py에 polls 앱의 path를 path(**"polls/"**, include('polls.urls'))로 등록해놨기 때문에
  - polls/urls.py에서 `polls/<int:question_id>/`라고 하지 않고 `<int:question_id> ` 만 작성해도 실제 url에서는 `http://127.0.0.1:8000/polls/2/results` 형식으로 정보가 넘어감



## 뷰 : 모델에서 정보 가져오기

- 템플릿은 일정한 형태로 정보들을 보여주기 위해 재사용할 수 있는 파일, 레이아웃을 의미한다. 장고의 템플릿 양식은 HTML!

- polls/view.py

  ```python
  from .models import Question
  
  def index(request):
      lastest_question_list = Question.objects.order_by('-pub_date')[:5]
      output = ', '.join([q.question_text for q in latest_question_list])
      return HttpResponse(output)
  ```

  - lastest_question_list  :  Question에서 최근 날짜에 작성한 질문들 5개를 가져와서 저장
  - output : .join() 을 활용해서 문장을 , (콤마)로 구분해서 붙이기

![view]({{site.url}}{{site.baseurl}}/assets/images/view-1.png)



## 템플릿으로 데이터 표현하기

- mysite/settings.py

  ```python
  TEMPLATES = [
      {
          'BACKEND': 'django.template.backends.django.DjangoTemplates',
          'DIRS': [],
          'APP_DIRS': True,
          'OPTIONS': {
              'context_processors': [
                  'django.template.context_processors.debug',
                  'django.template.context_processors.request',
                  'django.contrib.auth.context_processors.auth',
                  'django.contrib.messages.context_processors.messages',
              ],
          },
      },
  ]
  ```

- 장고의 템플릿 구조는 **polls/templates/polls/**index.html과 같이 이루어져 있다!

  - polls/templates/polls 처럼 만들어야 장고가 잘 알아들을 수 있음 (이름공간 name spacing)

- polls/templates/polls/index.html

  ```html
  {% if latest_question_list %}
  <ul>
      {% for question in latest_question_list %}
      <li><a href="/polls/{{question.id}}/">{{question.question_text}}</a>
      </li>
      {% endfor %}
  </ul>
  {% else %}
  <p>No polls are available</p>
  {% endif %}
  ```

- 템플릿에 맞게 polls/view.py의 index 뷰 업데이트하기

  ```python
  from django.template import loader
  
  def index(request):
      latest_question_list = Question.objects.order_by('-pub_date')[:5]
      template = loader.get_template('polls/index.html')
      context = {
          'latest_question_list': latest_question_list,
      }
      return HttpResponse(template.render(context, request))
  ```

  - 사실 render를 사용하면 더 편하게 할 수 있음...!



![view]({{site.url}}{{site.baseurl}}/assets/images/view-2.png)



![view]({{site.url}}{{site.baseurl}}/assets/images/view-3.png)



## render() 

> [참고](https://docs.djangoproject.com/ko/2.2/topics/http/shortcuts/#django.shortcuts.render)

- render(request, template_name, context=None, content_type=None, status=None, using=None)

- 템플릿에 context를 넣은 결과를 HttpResponse 객체와 함께 돌려주는 구문은 자주 쓰이기 때문에 이 용법을 쉽게 쓰도록 해주는 것이 render()

- 예를 들어서 아래와 같이 쓰임!

  ```python
  from django.shortcuts import render
  
  def my_view(request):
      # ...
      return render(request, 'myapp/index.html', {
          'foo': 'bar',
      }, content_type='application/xhtml+xml')
  ```



### HttpResponse로 작성했던 뷰view 수정

- polls/views.py

  ```python
  from django.shortcuts import render
  from .models import Question
  
  def index(request):
      latest_question_list = Question.objects.order_by('-pub_date')[:5]
      context = {'latest_question_list': latest_question_list}
      return render(request, 'polls/index.html', context)
  ```

  

