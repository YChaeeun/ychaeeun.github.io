---
title: web RESTful Api란?
date: 209-05-26
categories:
 - web
---





## REST 란?

- Representation State Transfer
- **분산 시스템 설계** 을 위한 소프트 아키텍쳐의 한 형식

- API에서 전송하는 자원(Resource)를 URI로 표현하고 해당 리소스에 행하고자 하는 의도를 HTTP 메소드로 정의하는 방식이다
  - URI  :  Uniform Resource Identifier 통합자원식별자 (인터넷에 있는 자원을 나타내는 유일한 주소)
- **REST 원리를 따르는 시스템을 RESTful 이라고 부른다**



## RESTful API

- 엔드포인트의 URI를 "/user"라고 정하고 POST로 HTTP 요청
	```
	POST /user
	{
		"id" : "ychae",
		"email" : "ychae@email.com"

	}
	```





## 장단점

- 장점
  - 자기 설명력 (self-descriptiveness)
  
    : 엔드포인트의 구조만 보더라도어떤 리소스와 기능을 제공하는지 쉽게 파악 가능
  
  - 단순하고, web 확장에 용이하다
  
  - 별도의 프로토콜 없이도 기존 HTTP 인프라를 사용 가능
  
- 단점

  - 특정 클라이언트에 맞추어져서 다른 클라이언트에 사용이 어렵다 (틀에서 벗어나기가 어려움)
  - 이런 문제를 해결하기 위해 페이스북을 **GraphQL**을 만듬!