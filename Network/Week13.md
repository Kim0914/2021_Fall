# 15. Internetworking Part 4
## IPv4 Mobility
* Definition of Internet: IP 프로토콜을 기반으로 하는 네트워크의 네트워크
* IoT: 모든 객체는 자신의 주소를 가지고 있다.
  * 그러면 객체가 움직이면 IP의 흐름은 어떻게 될까?

## IP Mobility issue
* 네트워크 층이 사용하는 프로토콜이 IP Protocol이다.
* IP주소는 계층적인 구조를 가지고 있다.
  * 2가지 부분으로 나뉘는데 **Network, Host** 2가지 부분으로 나뉜다
  * Class A,B,C,D,E로 나뉘어 지고 자세한건 강의자료 참고
* A,B,C의 네트워크가 있고 각각의 네트워크에 A1,B1,C1의 디바이스가 있다고 하자.
  * **A1 장치가 B1장치로 패킷을 전송하려고 하는데, B1 장치가 C 네트워크로 이동했다고 하면 어떻게 패킷이 전달될까?**
  * 각각의 장치들은 다른 장치가 움직였는지 모른다. 따라서 **Router를 이용해서 redirection을 해줘야 한다!!** 이것이 핵심이다.

## Mobility Management in Network Layer
* **1. Location Management: IP Network Layer**
  * 모바일 노드의 장소를 업데이트 한다.
  * 모바일 노드에서 나오는 비디오, 보이스 등의 데이터를 트래킹한다.
  * Network ID 부분이 모바일 노드의 위치를 의미하고, Host ID 부분이 모바일 노드의 식별번호를 의미한다.
* **2. Handover**
  * Handover은 서로다른 네트워크 간에 이동을 할 때(망에서 망) 연결이 끊어지는 것 없이 이동하는 것이다.
  * End to End Handover라고도 한다.

## Location Management: IP Network Layer
* **Routing**
  * IP address: Network ID + Host ID
  * IP 라우팅 알고리즘은 목적지 주소를 기반으로 한다.

* **Mobile Node**
  * Access point 에서 Access point로 이동할 수 있는 노드를 말한다. 예를 들면 휴대폰, 노트북?
  * 사용자라고 생각하면 편하다.

* **Home Address (HoA)**
  * 모바일 노드가 원래 있던 곳(초기에 있던 곳), 영구적인 IP 주소를 의미한다. HoA 라고 한다.
  * IP 주소는 초기에 home link에 할당되어진다.
  
* **Care of Address(CoA)**
  * 모바일 노드가 다른 링크(Foreign Link)로 이동하는 경우, 해당 링크를 current 링크로 설정한다.
  * Foreign Agent가 네트워크에 다른 놈이 왔다는 것을 인지하고 CoA를 할당한다.

* **Home Agent**
  * 모바일 노드가 다른 네트워크로 이동하여 CoA를 부여받았을 때, 원래 자신 네트워크의 라우터에 등록하는 것

* **Foreign Agent**
  * 모바일 노드가 다른 네트워크로 이동했을 때, 해당 네트워크의 라우터를 나타낸다.
  * FA가 HA로 CoA를 전송한다

* **Correspondent Node**
  * 모바일 노드가 패킷을 보내려고 하는 노드를 말한다.
### <요약>
* 처음에 모든 host와 라우터들이 전원을 키면 arp 메세지가 교환되고 각 기기는 arp 테이블을 그리게 된다.
* 이 과정이 끝나고 모바일 노드가 다른 네트워크로 이동했다고 하자.
* 이 상황에서 모바일 노드는 FA가 보내는 advertisement message를 듣고 FA가 존재하는지를 알게된다.
* 자신의 IP, MAC, HA의 주소를 FA에게 등록한다. 그리고 이 해당정보를 FA가 HA에게 누가 왔고, 앞으로는 나한테 보내달라고 알려준다.
* FA가 HA에게 나한테 보내달라고 하면서 보내주는 주소가 CoA이다.

* 다음부터 모바일 노드에게 오는 모든 메세지는 FA로 가야되고, HA는 proxy ARP처럼 동작해야 된다.
* HA가 FA에게 패킷을 전달해줘야 Dest까지 패킷이 도달할 수 있다.
* 따라서 HA는 FA까지 IP 터널링을 뚫는다. 기존의 패킷을 다시 래핑한다. -> 다시 새로운 Dest IP, SRC IP를 추가한다.
* FA에 이 패킷이 도달하면 추가된 패킷을 벗기고 기존의 패킷 내용을 확인하고 이더넷 프레임을 만들어서 보내면 된다.

* 모바일 노드가 반대로 보내는 경우라고 하자. 라우터는 항상 패킷의 목적지 주소만 확인한다. 출발 주소가 자신의 네트워크인지는 고려 x
* 라우터가 목적지 주소를 확인하고 해당 네트워크로 패킷을 포워드한다. 라우터는 그냥 자기가 원래 하던 일을 하는거다.

* 이동노드간의 통신이 일어난다고 하면, 둘 다 FA에 위치하고 있는 것이다. 
* 모바일 노드1이 모바일 노드2로 보낸다고 하면 FA1가 목적지 주소를 보고 해당 HA2로 보낸다. 
* 그러면 그 HA2는 자기의 모바일 노드가 FA2로 이동한 것을 알기 때문에 그 쪽으로 IP 터널링을 한다.
