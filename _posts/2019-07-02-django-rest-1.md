---
title : django rest framework -1 (설치 & Quick start)
date : 2019-07-02
catetories
 - django-rest-framework
---



### 더보기

> [Django REST framework Document](https://www.django-rest-framework.org/)



## 설치

- django가 설치되어 있고, django-admin startproject mysite . 도 실행했다고 가정 [참고](https://ychae-leah.tistory.com/131)

- django-rest-framework 설치

  ```shell
  $ pip install djangorestframework
  $ pip install markdown
  $ pip install django-filter
  ```

- mysite/settings.py 수정하기

  ```shell
  $ vim mysite/settings.py
  ```

  ```python
  INSTALLED_APPS = (
  	...
  	'rest_framework',  # 추가하기
  )
  ```

- mysite/urls.py 수정

  ```shell
  $ vim mysite/urls.py
  ```

  ```python
  urlpatterns = [
      ...
      url(r'^api-auth/', include('rest_framework.urls'))
  ]
  ```

  - url은 나중에 자신이 원하는 대로 수정하면 됨



## QUIK START 일단 한 번 해보자

- [참고](https://ychae-leah.tistory.com/131)

### 기본 세팅

  ```shell
# 작업 폴더 생성
mkdir django-rest-framework
cd django-rest-framework
  
# 가상환경 구축
python3 -m venv env
source env/bin/activate  
  
# 설치
pip install django
pip install djangorestframework
  
# 어플리케이션 생성하기
django-admin startproject mysite . 
cd mysite
# 뒤에 꼭 . 점을 찍어줘야해!
django-admin startapp quickstart
cd ..
  
# 데이터베이스 첫 sync
python manage.py migrate
  
# 슈퍼유저 생성
python manage.py createsuperuser
  ```

![rest-1]({{site.url}}{{site.baseurl}}/assets/images/rest-1.png)



### Serializers

>  [document](https://www.django-rest-framework.org/api-guide/serializers/#serializers)

- serializers는 복잡한 데이터들(queryset)이나 모델 인스턴스들을 JSON과 XML 등등으로 변환하기 쉽게 파이썬 자료형처럼 바꿔준다. 장고의 Form 이나 ModelForm과 비슷하게 사용

- Serializer : 응답 결과를 조정 / ModelSerializer : model 인트턴트나 쿼리셋 다룰  때 사용

- mysite/quickstart/ 폴더에 serializers.py 파일을 생성한다

  ```
  $ vim mysite/quickstart/serializers.py
  ```

  