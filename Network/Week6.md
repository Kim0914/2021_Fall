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
  
  
