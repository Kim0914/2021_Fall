## Cost-Effective Resource Sharing
* 모든 데이터가 디지털 데이터로 들어오게 되고, CPU나 메모리가 처리하게 된다
* 패킷 스위칭 네트워크는 디지털 통신을 위해 사용된다
* Multiple Input이 들어오고 Output Line은 하나이다
* ***어떻게 패킷 스위칭 네트워크에서 cost-effective하고 resource sharingg하게 할 수 있을까?***
  * **By Multiplexing and Demultiplexing**

* FIFO Packet Scheduling은 VOIP를 지원하는데 충분하다
* Voice data packet은 150ms 딜레이(Interarrival time)를 넘어가면 깨질 수 있다 -> VoIP의 Qos Requirement: 150ms
---
* Latency
  * Delay = Transmission delay + Propagation delay + Queueing delay + Processing delay
  * **Transmission: Sender가 네트워크 링크에 보내는데 걸리는 시간**
  * **Propagation: 거리에 따라, 매질에 따라 보내는데 걸리는 시간**
  * **Queueing, Processing: 도착한 라우터에서 Queueing 하고 Processing 하는데 걸리는 시간**
  * 패킷을 잃어버린 경우. 예를 들어 카톡에서 hello라고 보냈을 때 상대방은 hello를 수신하지 못함.
  * 나는 이 패킷이 사라진지 모르고 계속 이야기 함. ACK를 받지 못했기 때문에 재전송 할지, 삭제할지 선택하라고 함.
  * **Real time Service에서 재전송은 의미가 없다** -> 갑자기 이야기하는중에 hello를 보내면 뜬금 없다

* Jitter
  * 패킷 delay의 variation을 측정한다
  * 패킷간의 도착시간 차이의 정도인데, 예를 들어 Variance(50,50,50) = 0 이다. 즉 Constant 하다
  * 30ms가 넘는 Jitter는 Voice data packet에 영향을 줄 수 있다


* **패킹 스위칭을 할 수 있는 이유는, 모든 데이터(정보)가 디지털화(Digitalized) 되어져 있기 때문**

* Burst: 시간대에 따라 트래픽이 폭발적으로 증가하는 시간

* 패킷은 각각 독립적으로 움직인다. 라우터마다 처리하는 시간이 다를 수 있는데 패킷의 순서가 뒤바뀔 수 있다
 * 반드시 목적지에서 패킷의 Out of order를 조정해야 한다

* 출력보다 입력이 많은 경우 버퍼링이 필요하고 더 많은 패킷이 오는 경우 Congestion이 발생

## Packet Switching의 실생활 예시
![image](https://user-images.githubusercontent.com/68818952/135823368-9e77ea1a-6c8b-420b-8709-6408570e33d0.png)
* Packet(패킷)은 고속도로에서의 Vehicle(자동차)와 같다
* Router(라우터)는 고속도로에서의 Tollgate(톨게이트)와 같다
* Packet Scheduler(패킷 스케줄러)는 고속도로에서 Ticketing or High-Pass(표 발급)와 같다
* 도로에 차가 많다 -> 네트워크 혼잡
* 톨게이트에 차가 많다 -> 버퍼처리하는데 혼잡
* Resource sharing ->  양방향 통행

---
* IP: Best-Effort Packet Delivery
  * 패킷 스위칭은 패킷 내부에 있는 데이터를 보낸다.
  * src & dest의 주소를 헤더에 담아서 보내게 된다. 항상 최고의 노력으로 전달하려고 하지만, 안될 수도 있다
  * 패킷을 잃어버릴 수도 있고, 패킷이 손상될 수도 있고

* **TCP Connection**
  * TCP 연결은 반드시 1:1연결이다. 1:N으로 연결할 수 없다
  * 순서대로 진행하고, Reliable하다
  * **Byte 단위의 통신을 한다**
  ![image](https://user-images.githubusercontent.com/68818952/135824348-fbbc61ae-dd5f-45b6-8dc0-90e6e350164d.png)
  * 예를들어 "I am happy"라는 메세지를 보내는 경우
  * Seq가 92부터 시작하므로 I: 92, a: 93, ..., y: 99 이다
  * Host A는 Seq=92와 ACK를 요청하고, Host B는 크기 8바이트를 계산한 후 ACK=100을 보내달라고 응답한다.
  * 하나의 Line으로 양방향 통신을 할 수 있다(Full-Duplex)
  * Half-Duplex는 보내는 방향을 설정해야함(단방향)


