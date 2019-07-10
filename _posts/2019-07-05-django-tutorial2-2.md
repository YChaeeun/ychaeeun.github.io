---
title : django 튜토리얼2 -2 (데이터베이스 & 모델model & ORM)
date : 2019-07-05
categories:
 - django

---



> [document 첫 번째 장고 앱 작성하기](https://docs.djangoproject.com/ko/2.2/intro/tutorial02/)



## 데이터베이스 실행

- 장고는 기본적으로 sqlite를 제공하는데, 만약 다른 데이터베이스를 사용하고 싶다면 settings.py의 설정을 바꿔줘야 한다

- 데이터베이스 실행

  ```shell
  $ python manage.py migrate
  ```

  

## 모델 만들기

- 모델은 데이터베이스의 구조(layout) !!!!

- 설문조사 앱을 위해서 Question 과 Choice 라는 두 개의 모델을 만들어 보자

- polls/models.py

  ```python
  from django.db import models
  
  class Question(models.Model):
      question_text = models.CharField(max_length=200)
      pub_date = models.DateTimeField('date published')
      
  class Choice(models.Model):
      question = models.ForeignKey(Question, on_delete=models.CASCADE)
      choice_text = models.CharField(max_length=200)
      votes = models.IntegerField(default=0)
  ```

  - pub_date에 'date published'는 사람이 읽기좋은(human-readable) 이름을 지정해준 것 (?)
  - 장고는 기본적으로 **pk (Primary Key)**를 생성해주는데, id 값이라고 생각하면 됨! 데이터가 추가될 때마다 자동으로 증가하는 숫자 (ex. 1, 2, 3 ... )
  - **ForeignKey**(to, on_delete, **options)
    - many-to-one relationship  한 테이블 필드가 다른 테이블의 행을 참조한다는 의미! 
    - 위의 예시로는 Choice의 question 항목의 값은 Question 테이블에 있는 값을 참조하고, 가져올 수 있다!
  - ForeignKey(to, **on_delete**, **options) [참고]([https://ko.wikipedia.org/wiki/%EC%99%B8%EB%9E%98_%ED%82%A4](https://ko.wikipedia.org/wiki/외래_키))
    - 참조되는 테이블의 값이 변경되었을 때, 이를 참조하는 테이블은 어떻게 해야할지 정해둔 규칙 ( A, B : B의 행 b가 A를 참조한다고 가정한다면)
    - **CASCADE** : 참조하는 테이블의 행이 삭제되면 대응되는 행들도 같이 삭제, 갱신되면 같이 갱신 (A가 변하면 b도 같이 변해)
    - **RESTRICT** : 데이터 변경이 이뤄지지 않음! 참조하는 테이블의 행이 남아있는 경우 참조되는 테이블의 값을 변경할 수 없다 (b가 있는 한, A의 값을 변경할 수 없음)
    - NO ACTION : ?????
    - **SET NULL** : 참조되는 테이블이 갱신 혹은 삭제되었을 경우, 참조하는 행에 대한 외래 키 값은 NULL로 설정됨, 물론 NULL이 허용될 때만! (A가 변화하면 b는 NULL)
    - **SET DEFAULT** : 참조되는 테이블의 값이 변경되었을 경우, 참조하는 테이블의 값은 속성의 기본값(default)로 설정 (A가 변화하면 b는 b의 기본값으로)





## 모델 활성화하기



### 1) 프로젝트에 앱 등록하기

- mysite/settings.py

  ```python
  INSTALLED_APPS = [
      ...
      'polls.apps.PollsConfig'
  ]
  ```
  - polls/apps.py 에 보면 아래와 같이 나오는데, INSTALLED_APPS 에 **polls** 만 적어줘도 됨! (아래 name = 'polls'라고 하는 것을 보니 둘 다 같은 뜻인 듯)

    ```python
    # polls/apps.py
    from django.apps import AppConfig
    class PollsConfig(AppConfig):
        name = 'polls'
    ```
  
    

### 2) makemigrations & migrate

- 데이터베이스나 테이블에 직접 손을 대지 않고도 모델을 계속 변경할 수 있게 해준다! 현재 동작 중인 데이터베이스를 자료 손실없이 업그레이드 하는 데 최적화 되어 있음

- makemigrations : 모델을 변경시킨 사실과 이 변경사항을 **migration**으로 저장하고 싶다는 것을 django에게 알려준다

  - migration : 장고가 모델의 변경사항을 저장하는 방법으로, 디스크상의 파일로 존재함

  ```shell
$ python manage.py makemigrations polls
  ```

- migrate : 데이터베이스에 모델과 관련된 테이블을 생성

  ```shell
  $ python manage.py migrate polls
  ```

  



## 데이터베이스 살펴보기! ORM

> [장고 ORM 정리](https://ychae-leah.tistory.com/135)



- django interactive console 열기

  ```shell
  $ python manage.py shell
  ```

- 다루고 싶은 모델과 필요한 기능들을 import 해오기

  ```shell
  >>> from polls.models import Choice, Question
  >>> from django.utils import timezone
  ```

- 모델 보기

  ```shell
  >>> Question.objects.all()	# <QuerySet []>
  ```

- 데이터(객체) 생성 & 저장 & 값 보기

  ```shell
  >>> q = Question(question_text="Hello", pub_date=timezone.now())
  >>> q.save()
  
  >>> q.pk 	# 1
  >>> q.id 	# 1
  >>> q.question_text 	# "Hello"
  >>> q.pub_date			
  # datetime.datetime(2019,7,6,6,17,45,246028,tzinfo=<UTC>)
  ```
  
- 모델 보기 _ 의미있는 정보
  
  ```shell
  >>> Question.objects.all()	# <QuerySet [<Question: Question object (1)>]>
  ```
  
  - 표시되는 정보인 Question: Question object(1) 는 의미있는 정보가 아님! 의미있는 정보가 나올 수 있도록 모델을 수정해주면 됨
  - polls/models.py
  
  ```python
  from django.db import models
  
  class Question(models.Model):
     # ...
  	def __str__(self):
          return self.question_text
      
  class Choice(models.Model):
      # ...
      def __str__(self):
          return self.choice_text
  ```
  
  - 그리고 다시 장고 인터렉티브 셀을 실행하고 모델을 보면,
  
    ```shell
    >>> Question.objects.all()	# <QuerySet [<Question: Hello>]>
    ```
  
- 검색하기

  ```shell
  >>> Question.objects.fileter(id=1)	# <QuerySet [<Question: Hello>]>
  ```

  ```shell
  >>> current_year = timezone.now().year
  >>> Question.objdects.get(pub_date__year=current_year)
  ```

  - 던더스코어로 검색 특정조건을 추가할 수 있음 
  - 위의 예시는 "pub_date 중에서 year == curreunt_year 인 자료를 가져와"라는 의미



### choice_set [참고](https://stackoverflow.com/questions/2048777/what-is-choice-set-on-the-django-app-tutorial)

- 구성해놓은 두 가지 모델 Question과 Choice가 있는데, choice는 question을 참조한다. 이때 장고는 자동으로 두 테이블의 관계를 관리하는 field를 생성함 (RelatedManager)
- 이름은 **0000_set**  



