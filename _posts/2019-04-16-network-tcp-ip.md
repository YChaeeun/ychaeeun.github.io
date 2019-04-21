---
title: network TCP/IP 프로토콜
date: 2019-04-16
categories:
 - network
---



## TCP/IP 프로토콜이란?

> [출처](https://ko.wikipedia.org/wiki/인터넷_프로토콜_스위트)



+ TCP/IP는 인터넷의 공용어라고 할 수 있다
+ 각각 네트워크 호스트들의 고유 주소인 IP를 통해 다른 네트워크 안에 있더라도 데이터를 주고 받을 수 있도록 만들어 있다는 것이 특징이다.



## TCP/IP Layers & 프로토콜 스위트

> [출처](<https://www.ibm.com/support/knowledgecenter/ko/ssw_aix_71/com.ibm.aix.networkcomm/tcpip_protocols.htm>)



![tcp-ip-layers]({{site.url}}{{site.baseurl}}/assets/images/network-tcp-ip.png)



![tcp-ip]({{site.url}}{{site.baseurl}}/assets/images/tcp-ip.png)





## TCP/IP의 구성

+ TCP/IP 프로토콜은 아래 두가지 프로토콜로 이루어져 있다
  + 패킷 통신 방식의 인터넷 프로토콜인 **IP (Internet Protocol)**
  + 전송 조절 프로토콜인 **TCP(Transmission Control Protocol)**

+ IP는 패킷 전달 여부를 보증하지 않고, 패킷에서 보낸 순서와 받는 순서가 다를 수 있다.  
+ TCP는 IP 위에서 동작하는 프로토콜로, 데이터의 전달을 보증하고 보낸 순서대로 받게 해준다 !



