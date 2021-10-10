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
