---
title : django 정리-2 (모델 model)
date : 2019-07-03
categories:
 - django
---



> [django document](https://docs.djangoproject.com/ko/2.2/intro/tutorial02/#creating-models)



## 모델 Model

- 모델이란 부가적인 메타데이터를 가진 **데이터베이스의 구조(layout) **--> 장고는 ORM으로 데이터베이스의 데이터를 관리한다

  - ORM이란 객체과 관계형 데이터베이스의 데이터를 매핑해서 sql 쿼리문을 작성하지 않고 쉽게 데이터를 다룰 수 있게 해주는 것을 의미한다. [참고](https://ychae-leah.tistory.com/134)

- 장고는 DRY(반복하지 말 것!) 이라는 원칙을 가지고 있어서 데이터모델을 한 곳에 정의하고 유도할 수 있도록 하는 것이 목표

- 각 모델은 django.db.models.Model 이라는 클래스의 서브 클래스로 표현된다

- 모델을 선언한 뒤에는 데이터베이스에 해당 모델을 위한 테이블을 생성해야 하므로 migrate를 해줘야 한다

  ```shell
  $ python manage.py makemigrations <app>
  $ python manage.py migrate <app>
  ```

  

  

### 예를 들어서...

- Person이라는 모델을 선언하는 것은 곧 이러이러한 데이터베이스를 만들겠다는 의미가 된다

  ```python
  from django.db import models
  
  class Person(models.Model) :   # Person이라는 모델 객체 선언
      first_name = models.CharField(max_length=30)
      last_name = models.CharField(max_length=30)
  ```

  ```sql
  CREATE TABLE myapp_person (
  	"id" serial NOT NULL PRIMARY KEY,
      "first_name" varchar(30) NOT NULL,
      "last_name" varchar(30) NOT NULL
  );
  ```

  

## [모델의 필드 타입](https://docs.djangoproject.com/ko/2.2/ref/models/fields/#field-types)

- 데이터베이스의 각 필드는 Field 클래스의 인스턴스로 표현된다

- 몇몇 클래스들은 필수 인자가 필요한 경우도 있음 (문자 자료형은 자료의 길이 max_length를 입력해줘야함)

- options 다양한 선택적 인자를 가질 수도 있다 (ex) default=0

- **ForeignKey**

  - 모델 A, B 가 있다고 했을 때 값들의 관계를 알려준다 (many-to-one / many-to-many / one-to-one)

  - ??

    ```python
    class A (models.Model):
    	a = models.CharField(max_length=200)
    	
    class B (models.Model):
        b = models.ForeignKey(A, on_delete=models.CASCADE)
    
    ```

- 필드 타입 예시

  ```shell
  - CharField(max_length=None) 
  - TextField()
  - EmailField(max_length=254)
  - DateTimeField(auto_now=False, auto_now_add=False) 
  - FileField(upload_to=None, max_length=100)
  - IntegerField()
  ```

  



## 모델 활성화 하기

- 우선 모델의 app을 settings.py의 INSTALLED_APP = [] 목록에 적어서 등록해야 한다

- makemigrations `<appname>` 명령어를 통해 모델의 변경사항을 파악

  ```shell
  $ python manage.py makemigrations <appname>
  ```
	- migration 이란, 장고가 모델의 변경사항과 데이터베이스 스키마를 저장하는 방법을 의미한다
	
- **migrate**

  - migrate 명령어를 통해서 자동으로 migration을 실행시켜주고, 데이터베이스 스키마를 관리해준다
  - sqlmigrate는 내부에서 어떤 sql 문장을 실행하는지 직접 보여줌
  
  ```shell
  $ python manage.py migrate <appname>
  ```
  
  ```shell
  $ python manage.py sqlmigrate <appname>
  ```
  
  
  
  