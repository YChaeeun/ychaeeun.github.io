---
title : django 튜토리얼 -4 (pythonanywhere 배포)
date : 2019-07-02
categories:
 - django

---



 

### 더보기

> [1) 장고걸스 튜토리얼](https://tutorial.djangogirls.org/ko/)
>
> [2) django 튜토리얼 -1 (설치 & 서버 간단 구동)](https://ychae-leah.tistory.com/131)
>
> [3) djago 튜토리얼 -2 (어플리케이션&모델 생성)](#)
>
> [4) djago 튜토리얼 -3 (admin & superuser 생성)](#)



## github 에 코드 올리기



[참고](https://tutorial.djangogirls.org/ko/deploy/)



## pythonanywhere 배포

- pythonanywhere.com -> Beginner로 가입  후, pythonanywhere 콘솔 > $Bash 콘솔로 접속하기

### bash console

- git repository에 있는 코드 clone 해오기

  ```shell
  $ git clone https://github.com/<username>/<repositoryname>
  ```

  - 레포지토리 옆에 있는 초록색 clone or download 버튼을 눌러서 나오는 주소를 복사해서 붙여넣으면 됨 (https 통신 고르기)

- tree 를 통해서 복사해온 파일들의 구조를 볼 수 있음 (github repository 이름이 djangoTutorial)

  ```shell
  $ tree djangoTutorial
  djangoTutorial
  ├── blog
  │   ├── __init__.py
  │   ├── admin.py
  │   ├── apps.py
  │   ├── migrations
  │   │   ├── 0001_initial.py
  │   │   └── __init__.py
  │   ├── models.py
  │   ├── tests.py
  │   └── views.py
  ├── manage.py
  └── mysite
      ├── __init__.py
      ├── settings.py
      ├── urls.py
      └── wsgi.py
  ```

- 경로 이동 후 가상환경 생성 & 실행

  ```shell
  $ cd djangoTutorial
  $ virtualenv --python=python3.7 myvenv
  ```

  ```shell
  $ source myvenv/bin/activate
  ```

- 장고 설치

  ```shell
  $ pip install django~=2.0
  ```

- 데이터베이스 생성하기

  ```shell
  $ python manage.py migrate
  ```

- 슈퍼유저 생성하기

  ```shell
  $ python manage.py createsuperuser
  ```

- ALLOWED_HOST 에 pythonanywhere 추가하기

  ```shell
  $ vim mysite/settings.py
  ```

  - 파일에 들어가서 ALLOWED_HOST =['127.0.0.1', '.pythonanywhere.com'] 으로 수정



## Add a new web app

- 도메인 주소를 확정한 다음 대화창에서 **수동설정(manual configuration)**  을 선택하고 **python3.7** 선택
  - 기본 설정에서는 Django를 고르지 않는게 더 좋다고 함!

- 가상환경 path 입력
  - Virualenv 탭에 주소를 아래와 같이 입력한다
  - /home/`<yourname>/<your_repository_name>/myvenv`



## WSGI 파일 설정하기

- 장고는 WSGI 프로토콜을 사용한다
- web app 탭에서 Code 섹션 부분의 WSGI configuration file 의 링크를 클릭한다
  - 그다음 나오는 파일을 쭉 내려보면 Django 각주가 되어 있을텐데, 코드 부분의 각주를 하나하나 해제해주면 된다 (코드 앞에 붙은 #를 지워줌)
  - 그리고 저장



## 배포 끝!

![wow]({{site.url}}{{site.baseurl}}/assets/images/wow.png)