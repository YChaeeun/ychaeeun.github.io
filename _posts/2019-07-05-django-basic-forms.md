---
title: : django 정리-4 (장고 폼 forms)
date : 2019-07-05
categories:
 - django
---



> [django documents-forms](https://docs.djangoproject.com/ko/2.2/topics/forms/#django-s-role-in-forms)
>
> [django documents - modelform](https://docs.djangoproject.com/ko/2.2/topics/forms/modelforms/#modelform)



## 폼 forms

- 장고의 폼으로 강력한 인터페이스를 구축할 수 있는데, 복잡한 여러 과정들을 간결하게 그리고 자동으로 처리해준다
- 폼form은 크게 세가지 역할을 수행해준다 (물론 개발자가 직접 코드를 입력해서 처리할 수도 있고)
  - rendering 할 수 있도록 데이터를 준비하고 재구성
  - HTML form 생성
  - 클라이언트로부터 데이터를 전달받고, 처리해줌



## ModelForm

- 특별한 준비가 없어도 폼 양식을 만들고, ModelForm을 생성해서 자동으로 모델에 결과물을 저장할 수 있다!

- blog/forms.py

  ```python
  from django import forms
  from .models import Post
  
  class PostForm(forms.ModelForm):
      class Meta:
          model = Post
          fields = ('title', 'text',)
  ```

  - forms와 Post 모델을 import
  - forms.ModelForm  :  해당 폼이 모델 폼이라는 것을 알려줌
  - class Meta : model = Post : 폼을 만들기 위해 어떠한 모델을 사용할 것인지 알려주는 역할
  - fields : 해당 폼에서 어떤 요소들을 보여지게 할 것인지

![fields]({{site.url}}{{site.baseurl}}/assets/images/form.png)



