---
title: network 프로토콜 protocol 기본
date: 2019-04-16
categories:
 - network
---



## 프로토콜 Protocol

- 컴퓨터 간에 정보를 주고받을 때 사용하는 통신 방법의 **규칙**이나 **표준**
- 컴퓨터는 프로토콜이 같은 것끼리 통신을 주고 받을 수 있다
- __프로토콜 슈트 (protocol suite) __
  + 통신 규약 (프로토콜)의 모음을 의미한다.
  + 대표적인 인터넷 프로토콜 슈트는 **[TCP/IP 프로토콜](<https://ychaeeun.github.io/network/network-tcp-ip/>)**이 있다



## 프로토콜의 구성

프로토콜은 두 가지로 이루어져 있다. [출처](<https://ko.wikipedia.org/wiki/%ED%86%B5%EC%8B%A0_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C#%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C%EC%9D%98_%EA%B5%AC%EC%84%B1>)

+ 물리적 측면

  + 자료 전송에 쓰이는 전송 매체, 접속용 단자 및 전송 신호, 회선 규격 등등

+ 논리적 측면

  + 프레임 구성, 프레임 안에 있는 각 항목의 뜻과 기능, 자료 전송의 절차 등등

  + 폐쇄적인 프로토콜: 자사 장치들끼리 통신하기 위한 독자적 통신 규약으로 크래킹 위협에 상대적으로 안전하다

    >  ex. IBM의 SNA, SDLC 프로토콜

  + 공개적인 범용 프로토콜 : 여러 장치들에 쓰이는 널리 알려진 규격으로, 컴퓨터와 크래킹에 취약한 편이다

    > ex. 인터넷의 TCP/IP





## OSI 7 Layers 각 계층의 프로토콜

> [출처](<https://ko.wikipedia.org/wiki/%EC%9D%B8%ED%84%B0%EB%84%B7_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C_%EC%8A%A4%EC%9C%84%ED%8A%B8>)



<table>
    <tr>
        <th>계층</th>
        <th>프로토콜</th>
    </tr>
    <tr>
        <td>응용계층</td>
        <td> <strong/>HTTP</strong/>, SMTP, SNMP, FTP, 텔넷, SSH & Scp, NFS, RTSP</td>
    </tr>
    <tr>
        <td>표현계층</td>
        <td>XDR, ASN.1, SMB, AFP</td>
    </tr>
    <tr>
        <td>세션계층</td>
        <td>TLS, SSL, ISO 8327 / CCITT X.225, RPC, 넷바이오스, 애플토크</td>
    </tr>
    <tr>
        <td>전송계층</td>
        <td><strong>TCP</strong>, UDP, RTP, SCTP, SPX, 애플토크</td>
    </tr>
    <tr>
        <td>네트워크계층</td>
        <td><strong>IP</strong>, <strong>IPX</strong>, ICMP, IGMP, X.25, CLNP, ARP, RARP, BGP, OSPF, RIP,DDP</td>
    </tr>
    <tr>
        <td>데이터링크계층</td>
        <td><strong>이더넷</strong>, 토큰링, PPP, HDLC, 프레임 릴레이, ISDN, ATM, 무선랜, FDDI</td>
    </tr>
    <tr>
        <td>물리계층</td>
        <td>전선, 전파, 광섬유, 동축케이블, 도파관, PSTN, <strong>리피터</strong>, DSU, CSU, 모뎀</td>
    </tr>
</table>






