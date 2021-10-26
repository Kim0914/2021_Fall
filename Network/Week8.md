## RARP - BOOTP - DHCP

### Proxy ARP
![image](https://user-images.githubusercontent.com/68818952/138815102-2f66022e-bfc0-483b-a6e7-f0457d3ed66f.png)
* Proxy: 가짜의, 대리인
* 프록시 ARP는 라우터가 ARP Request에 답(Reply)을 할 수 있도록 해준다
* Source와 Destination이 다른 네트워크에 있는 상황에서도 사용할 수 있다
  * 예를들어 Ethernet <-> USB 가 있다
* 이더넷에서는 이더넷 인터페이스와 연결되어있고, USB에서는 USB로 연결되어 있고 USB을 가진 임베디드 시스템이 있다
* 임베디드 시스템은 IP: 5, Src 시스템은 IP: 10 이라고 하자
* 이더넷 프레임을 보내기 위해서는 Dest MAC이 반드시 있어야한다
  * ARP Request를 보내야 함. "누가 IP 5를 가지고 있냐"를 보내면 프록시 ARP가 "내가 가지고 있다" 라고 말한다
  * ARP(라우터)의 주소 정보는 IP:1, MAC: B라고 가정한다
  * 그렇게 되면 Src의 ARP Table에는 <<IP: 5, MAC: B>>라고 기록된다
  * 이더넷프레임이 ARP에 도착하게 되면 운용되고 있는 Gateway program에서 알아서 처리한다


### Gratuitous ARP
![image](https://user-images.githubusercontent.com/68818952/138818378-966d2da8-91ef-45db-af4d-a1a999c2bc62.png)
* 시스템이 부팅될 때 OS는 시스템에 할당된 IP 주소가 다른 host에 의해 사용되는지 체크함(ARP Request)
  * "Who has my IP 10" -> **응답이 없으면 유일한 IP, 응답이 있으면 누군가가 쓰고 있는 것**
  * Broadcasting 방식으로 보내고 본인이 보내는 요청이기 때문에 본인의 IP 정보를 헤더에 담는다 Target IP도 내 주소
  * 응답이 오게되면 IP를 바꾸라고 OS가 메시지를 보낸다
