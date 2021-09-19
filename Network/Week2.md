## TCP/IP Protocol suite, Layer Concept


![image](https://user-images.githubusercontent.com/68818952/132973555-97e2121c-6841-46ef-b663-95c85775c86b.png)
* 카카오톡에서 메세지를 보낸다고 생각해보면, 카카오톡 소프트웨어를 먼저 사용해야한다.
* 카카오톡에서 메세지를 보내는 경우 하부 네트워크가 어떻게 동작하는지는 사용자는 관심이 없다
* 물리적으로는 소프트웨어(Application Layer) -> 전송 층 -> 네트워크 층 -> 데이터 링크 층 -> 물리적 층 을 거쳐서 가는 것
* 가상적으로는 ***Application Layer***에서의 **peer to peer view**. 즉, 상대방과 나의 관점을 horizon 하게 볼 수 있다.
* **상대방과 통신해야함**
  * **Process(port #) to Process(port #) delivery**가 필요한데 이 통신은 ***Transport Layer***에서 지원
* **내 시스템과 상대방 시스템 사이의 메세지 전달**이 필요함 
  * **end to end delivery** 이 통신은 ***Network Layer***에서 지원
* 종단과 종단이 바로 연결되면 좋지만, **물리적으로 거리가 멀어 불가능한 경우 중간지점에서 hop**이 필요함
  * **hop to hop delivery**가 필요하고 이 통신은 ***Data Link Layer***에서 지원


---
## TCP/IP Layer 요약 그림
![image](https://user-images.githubusercontent.com/68818952/132974145-97c18beb-5592-49a5-9034-ff933e92532d.png)


## Data Link Layer
![image](https://user-images.githubusercontent.com/68818952/132974448-f71af9e4-a401-45c7-8d50-423d465113d7.png)

* LLC (Logical Link Control)
  * Link control to support reliable communications between node and other nodes on the same link
  * error control, flow control, congestion control
  * We need 3 controls !! to support reliable communications


* MAC (Media Access Control)
  * ALOHA, Slotted ALOHA, CSMA/CD, CSMA/CA ...

* Why do we need MAC Address ?
  * => just use IP Address 
  * MAC Address guarantee the unique MAC Address

* Why do we need a router in the network?
 * 라우터는 서로 다른 네트워크 사이에서의 연결이라고 하자
 * 여기서 서로 다른 네트워크라는 것은 물리적으로 네트워크가 분리되어있는 것
 * => ***서로 다른 네트워크를 상호연결하기 위해 라우터 사용***

## 예를들어 컴퓨터공학관 <-> NC 백화점 물리적으로 분리된 서로 다른 두 네트워크를 연결하는 방법
 1. physical layer를 서로 연결 => 단순히 선만 연결, 신호가 약해지면 Repeater 혹은 Amplifier 사용 (Layer 1 Switch)
 2. DataLink Layer 끼리 연결 => 하나의 Network Device를 넣고 서로 선으로 연결, 각각의 interface에서는 Physical, MAC, LLC 존재 (Layer 2 Switch, Bridge, Hub)
 3. 공통된 Network Layer를 만들어서 연결 => Router (Layer 3 Switch, 모든 device는 IP를 가짐)
 4. Transport Layer에서 연결 => Gateway (Layer 4 Swtich)
 5. Application Layer에서 연결 => Packet을 받아서 다른쪽 방향 network로 재전송 (Layer 5 Swtich, gateway)

---
## 각각의 Layer에서 전달되는 data unit이 불리는 이름
![image](https://user-images.githubusercontent.com/68818952/133917394-b8b46006-df13-4e0d-93f4-1c4ee49e466b.png)

* Application Layer : Message
* Transport Layer : segment(TCP), datagram(UDP)
* Network Layer : packet
* Datalink Layer : Frame
