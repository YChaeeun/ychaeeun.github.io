---
title: network 캡슐화 & 역캡슐화 (encapsulation & decapsulation)
---



## 캡슐화 & 역캡슐화

+ 캡슐화 encapsulation
  + 송신 데이터에 필요한 정보 (헤더) 를 붙여서 다음 계층에 보내는 기술을 의미한다

  + 상위 --> **통신 프로토콜 정보 추가** --> 하위

  > 헤더 
  >
  > + 각 계층에서 수행한 정보들이 담겨있다 (데이터를 받을 상대에 대한 정보들도 포함되어 있음)
  >
  > + 데이터의 내용이나 성격을 식별하거나 제어하는 데 사용된다.

  

+ 역캡슐화 decapsulation
  + 캡슐화의 반대 개념으로, 헤더를 제거하는 것을 역캡슐화라고 한다
  + 하위 --> **헤더 제거** --> 상위



![capsulation]({{site.url}}{{site.baseurl}}/assets/images/encap.png)

