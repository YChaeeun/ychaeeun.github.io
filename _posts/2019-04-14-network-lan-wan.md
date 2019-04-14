---
title: network LAN & WAN 랜과 왠
last modified: 2019-04-14
categories:
 - network
---



## LAN vs WAN

<table>
  <tr>
    <th>LAN</th>
    <th></th>
    <th>WAN</th>
  </tr>
  <tr>
    <td>Local Area Network<br/>
      건물 안이나, 특정 지역의 <strong>좁은</strong> 네트워크</td>
    <th>범위</th>
    <td>Wide Area Network<br/>
      ISP를 통해 구축된 <strong>넓은</strong> 네트워크</td>
  </tr>
  <tr>
      <td>빠름(케이블 연결)</td>
      <th>속도</th>
      <td>느림</td>
  </tr>
  <tr>
      <td>적음</td>
      <th>오류</th>
      <td>많음</td>
  </tr>
</table>



### ISP

- Internet Service Provider 인터넷 서비스 제공자
- ex) KT, SKT, U+



## 가정에서의 네트워크

- 인터넷을 사용하기 위해서는 1) 인터넷 서비스 제공자(ISP) 2) 인터넷 회선 을 결정해야 함!

- 인터넷 공유기 == 가정용 라우터 (broadband router)



![homenet]({{site.url}}{{site.baseurl}}/assets/images/homenet.png){: .align-center}



## 작은 기업에서의 네트워크

- DMZ (Demilitarized Zone) : 외부 공개 서버
  - 외부네크워크(인터넷)과 내부 네트워크 사이의 중간 지대 __서브넷_
  - 네트워크의 보안 영역으로, 외부 공격자가 내부 네트워크에 침투하는 것을 막는다.
- 서버를 운용하는 방법 두 가지!
  - 클라우드
  - 온프레미스(On-premise) : 데이터센터 or 사내에 서버 장비실 구축



![officenet]({{site.url}}{{site.baseurl}}/assets/images/officenet.png){: .align-center}