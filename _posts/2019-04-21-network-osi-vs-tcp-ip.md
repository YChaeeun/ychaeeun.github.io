---
title: network OSI와 TCP/IP 차이점
date: 2019-04-21
categories:
 - network
---



>  [참고](<https://www.quora.com/What-is-the-relationship-between-the-OSI-reference-model-and-the-TCP-IP>)



## OSI vs TCP/IP



![osi-vs-tcp-ip]({{site.url}}{{site.baseurl}}/assets/images/network-osi-vs-tcp.png)



### OSI

- OSI 모델은 추상적이고, 보다 교육적인 목적(?)으로 네트워크 전반을 설명하기에 더 적합하다.
- OSI 모델의 1,2,3,4 계층은 데이터의 **전송**을 담당하고, 5,6,7 계층은 데이터의 **생성**을 담당한다.
- 구조가 복잡하여 망 설계시 상황 변화에 유연하게 대처하기가 어려움 (실생활 적용에 적합하지 않음)



### TCP/IP

- 반면 TCP/IP 모델은 OSI 모델을 바탕으로 실생활에 사용하기 위해 만들어졌다. (OSI는 참고용)
- 현재 인터넷은 TCP/IP를 사용하고 대부분의 통신 프로토콜은 TCP/IP !!