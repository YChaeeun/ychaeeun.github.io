---
title : django 튜토리얼2 -5 (404 에러 발생시키기)
date : 2019-07-09
categories:
 - django
---



> [document 첫 번째 장고 앱 작성하기](https://docs.djangoproject.com/ko/2.2/intro/tutorial03/)
>
> [document - Returning errors](https://docs.djangoproject.com/ko/2.2/topics/http/views/#returning-errors)





## 404 에러 일으키기

- 뷰에 태클걸기!
- 만약 요청된 질문의 ID가 없을 경우에 Http404 예외를 발생시키도록 detail 뷰 수정
  - HTTP 응답 코드 404는 클라이언트에 요청된 페이지를 표시할 수 없을 때 사용하는 응답 코드
  - [HTTP 응답 코드](https://ychae-leah.tistory.com/84)

- polls/views.py

  ```python
  from django.http import Http404
  
  # ...
  def detail(request, question_id):
      try:
          question = Question.objects.get(pk=question_id)
      except Question.DoesNotExist:
          raise Http404("Question does not exist")
      return render(request, 'polls/detail.html', {'question': question})
  ```

- polls/templates/polls/detail.html

  ```html
  {{question}}
  ```

  - 결과를 화면으로 볼 수 있게 detail.html 생성



![404]({{site.url}}{{site.baseurl}}/assets/images/error-1.png)

- ID가 없으면 우리가 작성한 Question does not exist 메시지가 출력된다 (현재 settings.py에 DEBUG=True라서 장고에서 이런 404 페이지를 생성해줌)





## 간단하게! get_object_or_404()

- 객체가 존재하지 않을 때 예외를 발생시키는 것은 자주 쓰이는 용법이기 때문에 단축 기능이 있음!

- polls/views.py

  ```python
  from django.shortcuts import get_object_or_404, render
  from .models import Question
  
  def detail(request, question_id):
      question = get_object_or_404(Question, pk=question_id)
      return render(request, 'polls/detail.html', {'question' : question})
  ```



![404]({{site.url}}{{site.baseurl}}/assets/images/error-2.png)