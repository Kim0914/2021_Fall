## Internet Design: Network Service Model
* What is the service model?
  * Ethernet/Internet: **best effort** -> packet can get lost (무책임하다)
* What if you want more?
  * Performance guarantees (QoS) are required... How?
  * Reliablity
    *  Corruption -> IP/TCP checksums
    *  Lost packet -> Retransmission

  * Flow and congestion control
    * Flow는 TCP에서는 리시버, Cn 는 소스가
  * Fragmentation
    * 하부 피지컬 레이어가 최대 1500바이트 까지라면, IP 패킷들이 쪼개질 수 있다
    * IP 프로토콜에서는 라우터가 fragmentation을 한다 -> 서로 다른 네트워크를 연결하기 때문에
    * 라우터는 Reassemble은 절대 하지 않는다 (라우터는 forwarding해서 빨리빨리 패킷을 처리해야 하는데 어셈블할 시간이 없음)
    * 오직 Destination이 fragemented IP packet을 reassemble 한다
  * In-oreder delivery
    * In-order delivery를 하기 위해서 Sequence number를 이용한다 (Seq #) 

![image](https://user-images.githubusercontent.com/68818952/136667516-d3d9785b-16bd-4709-be68-e55d2c79b8a6.png)


![image](https://user-images.githubusercontent.com/68818952/136667320-9717db26-0e53-4751-8061-a5f43464a672.png)

* Destination과 reliable한 connection을 유지하기 위해서는, 라우터들 사이에 queue들을 유지해야 한다
  * We need make queue reservation !!

* 인터넷 전화가 유선 전화보다 음질이 안좋은 이유
  * 유선 전화는 delay가 50ms이지만, 인터넷 전화는 delay가 150ms이기 

## Question: Who will make a resoure reservation
  1. Source
  2. Destionation
  Answer: **2. Destination**
  
  
## Layering: A Modular Approach
* Each Layers don't care about other layers (Independent)
* 상위 하위 모듈에 대한 API를 정의해야하고, 모듈 자체에 정의해야한다
* 기본적으로 Peer to Peer. 패킷은 수직적인 흐름, 프로토콜은 수평적인 흐름
* 프로토콜은 1. service interface 2. Peer-to-Peer interface 두가지 요소를 가진다

## Multiplexing and Demultiplexing
* 패킷이 IP 프로토콜(네트워크 층)에 도착하면 상위 레이어인 전송층 TCP, UDP, RTP 중 어디로 갈지 결정해야함
* IP 헤더에 그 정보가 담겨있다(Protocol Field) **Demultiplexing Key 라고도 한다**
* 프로토콜 필드는 Sender가 작성하고, Receiver가 사용한다
* IP Protocol의 모양이 모래시계와 비슷한데, 네트워크 레이어 상하부에 많은 것들이 정의되고 사용되기 때문
* 상하부 네트워크를 연결하는 역할이 네트워크 층이 하는 것이다
* IP Protocol은 Best Effot이면서 Unreliable하다

## 프로토콜에 대한 Standard를 정의하는 기구
1. IEEE: DataLink, Physical Layer (Institute of Electrical and Electronics Engineers)
 * Wireless, Ethernet, Bluetooth (e.g IEEE 802)
2. IETF: Network, Transport, Application (Internet Engineering Task Force)
 * TCP(RFC 793), IP (e.g RFC # - 표준문서)


---
## ARP (Address Resolution Protocol)
### Packet Encapsulation
* Assume Ethernet -> make a frame: Framing(데이터 링크층 에서 만듬)
* Address Resolution provides a mapping between two different forms of addresses
* ARP is a protocol used to do address resolution in the TCP/IP protocol suite(RFC826)
  * ARP는 IP address가 상응하는 Hardware address(MAC, Ethernet)를 연결하는 **dynamic mapping**을 제공한다

  ![image](https://user-images.githubusercontent.com/68818952/136750149-5d930332-e4e9-44fe-ae3e-347818fea9d3.png)
  * Ethernet Frame: Frame Header(22 bytes), IP Header(20 bytes), TCP/UDP Header(20 bytes), Data(1460 bytes), Frame Trailer(CRC, 4 bytes) 
    * Frame Header(22 bytes): Preamble(8 bytes), Dest addr(6 bytes), Src addr(6 bytes), Type(2 bytes)
      * Preamble: Frame의 시작을 나타내기 위해 사용되는 부분
      * Dest addr: Mac Address or Physical Address
      * Src addr: Mac Address
      * Type: 프레임이 Data link에서 Network Layer로 도착했을 때, IP or ARP 어디로 갈지 결정해야 할 때 Demultiplexing keys로 사용되기 위한 부분
        * IP: 0x8000, ARP:0x0806

* Ethernet Frame: 같은 네트워크에서 컴퓨터 대 컴퓨터로 통신하는 것
  * 각각의 디바이스는 유니크한 MAC를 가지고 있다 (48 bits)
    * Example: 00-C0-4F-48-47-93

![image](https://user-images.githubusercontent.com/68818952/136753134-689e57a0-897b-4ba0-b6c9-a1bec91a7daa.png)
* Question: ***컴퓨터 1이 어떻게 목적지(컴퓨터 B)의 MAC Address를 알 수 있을까?***
  * Answer: ARP Protocol을 통해 알 수 있다
  * ARP에 컴퓨터 1의 IP, MAC address와 컴퓨터 2의 IP address를 입력하면, ARP를 통해 컴퓨터 2의 MAC address 반환

![image](https://user-images.githubusercontent.com/68818952/136757541-5e0a68bd-47ac-47b4-bd08-5e3a9ace6514.png)
* 1. 컴퓨터 2는 컴퓨터 1이 언제 데이터를 전송할지 모른다
* 2. 컴퓨터 2는 링크를 항상 신호가 들어오는지 주시하고 있어야 한다
* 3. 어떤 신호가 도착해야 해당 신호를 받아들여 데이터링크에 올릴까?
* 4. 컴퓨터 1이 특정 패턴('10101010' 이 7번 반복(Preamble)되고, 마지막 바이트로 '10101011(SFD)'가 붙어서, 모두 8 바이트)을 제공해줘야 한다.


---
* ARP는 이더넷을 위해 디자인 된 것이 아니라, 데이터 링크 층을 위해 디자인 된 것이다
* 그러나, 데이터 링크 레이어는 "BroadCasting" 능력이 있어야만 한다
  * Broadcast: any data can be transmitted within on-hop range network
  * 이 네트워크를 LAN이라고 한다

## Dynamic Mapping
* IP Address can be changed easily by hand
* MAC Address는 unique하므로 이 IP Address와 MAC Address를 매핑시켜주는 역할을 한다
