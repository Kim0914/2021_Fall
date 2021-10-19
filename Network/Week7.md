# ARP Idea
* 기본 생각 Start
  * 내가 **패킷을 보내고 싶으면 하부 데이터링크 데이터로 바꿔야 한다**
  * 데이터링크가 이더넷이면, 이더넷 프레임으로 바꾸어야 한다
  * 이더넷은 **src 맥주소**와 **dest 맥주소**가 필요하다 -> **상대방의 맥주소를 알아야한다**
  * 우리가 기본적으로 통신할 때 상대방의 IP 주소는 알고있다고 합리적으로 가정한다
    * Why? 우리가 택배를 보낼 때 기본적으로 상대방의 주소는 알고있다고 생각하잖아
    * 나머지 중간중간에 들리는 영업소는 택배 시스템에서 알아서 해줌
  
* ARP는 multi-access channel을 필요로 한다. 즉 Broadcasting이다
* ARP 프로토콜을 간단히 설명하면
  * Sender가 Dest의 IP 주소를 가지고 있는 패킷을 ***broadcast*** 한다
  * 그 주소를 가진 machine은 MAC(HW) address를 포함하는 ***reply(unicast)*** 를 보낸다
  * MAC(HW) 주소는 오리지널 패킷을 보내기 위해 사용된다
---
## Broadcast-enable Network
* Broadcast request
  * 브로드캐스트는 같은 네트워크 서식지에 있는 모든 PC들에게 데이터를 주는 방식
  * 받는 PC의 주소는 모르고 IP 주소만 알고있을 때, 받는 PC의 MAC주소를 알아내기 위해 브로드캐스트를 날림
  * IP주소를 이용해 MAC주소를 받는 과정, 이 과정을 ARP라고 한다
  * 즉 패킷, 프레임을 받는 PC의 MAC 주소가 실제 프레임에 적혀있는 MAC 주소와 일치하지 않더라도 폐기하지 않음
  * 너무 많은 브로드캐스팅은 네트워크에 많은 혼잡을 야기함
* Unicast response
  * 유니캐스트는 1:1로 데이터를 전달하는 통신 방식. 
  * 데이터를 보내는 PC는 자신의 MAC 주소를 적고 받는 쪽 PC의 MAC주소도 적어 Frame에 감싸 데이터를 전달한다
  * Shared한 통신 방식을 취하기 때문에, 일단 같은 네트워크 서식지에 있는 모든 PC는 프레임을 받게된다
  * 각각의 PC는 받는쪽 MAC 주소와 자신의 LAN 카드 MAC 주소를 비교하여 같으면 CPU에 올리고 다르면 폐기한다

* ARP Procedure
  * **기본적으로 signal(신호)는 Broadcast이다** -> ***request이든 response이든 신호는 항상 누구에게나 전달된다!!!!***
  * 받는 대상(수신자)의 주소가 Broadcast인지 unicast인지에 대한 구별을 해야한다
  * "여러분 **누가** 이 IP주소를 가지고 있죠?" -> Broadcast
  * "**존 선생님** 제가 가지고 있어요!" -> Unicast
  * ARP is working on Ethernet
  * Ethernet has a broadcast capability
    * ***Sender(request): "physical address가 141.23.56.23인 노드를 찾고 있어요 !!" (Broadcast address)***
    * ***Receiver(response): "I am node you ard looking for and my physical addreess is: A46R F459 83AB" (unicast)**


## ARP Packet and Encapsulation of ARP Packet
![image](https://user-images.githubusercontent.com/68818952/137331147-c1cac882-2435-4c19-9882-1d5c9b61c53e.png)
* **Hardware Type**: Physical Layer가 어떤 타입인지 나타냄 -> 1: Ethernet
* **Protocol Type**: 상위 주소 타입이 어떤 타입인지 -> IP protocol:0x0800 and so on....
* **Hardware Length**: Physical address의 주소 길이 -> Ethernet: 6 bytes
* **Protocol Length**: Protocol의 길이 ->  IP address: 4 bytes
* **Operation**: 보내는 형식이 어떤 형식인지 -> 1: Request, 2: Reply, 3/4: RARP req/reply 
* ***ARP 패킷을 Ethernet Frame에 담는다***

## ARP Request/Reply
* **Ethernet dest addr**: ff:ff:ff:ff:ff:ff (broadcast) for ARP request
* **Ethernet src addr**: ARP request's address
* **Frame type**
  * ARP request/reply: 0x0806
    * ARP(Dest IP) -> Dest Mac addr
  * RARP request/reply: 0x8035
    * RARP(Dest MAC) -> Dest Ip addr
  * IP datagram: 0x0800 

## ARP Table
* 주어진 IP addr로 ARP 프로토콜을 이용해 MAC addr를 얻을 수 있는데, 이 정보를 유지하는 테이블을 ARP Table이라고 한다
* <IP address; MAC address; TTL> 데이터베이스 테이블 형식으로 존재해 ARP DB Table이라고도 한다
* IP address가 PK의 역할을 한다.
* TTL 만큼의 시간이 지나면 이 데이터는 테이블에서 제거된다

## ARP를 통한 패킷 전달과정 요약
1. 시그널이 브로드캐스팅 된다
2. 같은 네트워크에 있는 각각의 시스템(PC)이 Dest MAC 주소를 확인하고 request임을 확인 후 Accept
3. 각각의 시스템(PC)이 Target IP를 확인한다
4. 자신의 IP 주소와 비교
5. 본인의 주소와 일치하지 않으면 ARP request 패킷을 버리고
6. 본인의 주소와 일치하면 ARP Reply 패킷을 보낸다

## ARP통신을 하는 케이스
1. Src와 Dest가 같은 네트워크에 있는 경우: 일반적인 ARP 프로토콜을 하면 된다
2. Src와 Dest가 다른 네트워크에 있는 경우: Src와 해당 네트워크의 Default 라우터와 ARP 통신을 한다
3. Src의 네트워크 라우터와 Dest의 네트워크 라우터와: 서로 다른 네트워크에 패킷을 전달하기 위해서 라우터끼리 ARP 프로토콜
4. Dest의 네트워크 라우터와 Dest: Dest의 네트워크 라우터와 Dest 간의 ARP 통신을 해서 Dest의 MAC 주소를 알아내서 Reply한다

## 라우터와 ARP Table
* Broadcast-enable Network에서 같은 **_네트워크에 있는 사용자(PC)가 전원을 키면 자동으로 해당 네트워크의 라우터와 ARP request/reply_**
* Default 라우터는 자동으로 사용자(PC)의 IP 주소와 MAC 주소를 ARP Table에 담고 있다
* 사용자(PC)도 현재 네트워크상에 있는 ARP Table 정보를 각각 가지고 있다.
* 만약 한 사용자(PC)가 IP 주소가 바뀌면, 그 사용자가 본인의 IP와 MAC을 <IP, MAC>으로 broadcasting(ARP Reply)한다
* Broadcasting으로 보내기 때문에 Dest Mac은 111111111111로 담아서 Reply를 보낸다
