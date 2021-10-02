## Cost-Effective Resource Sharing
* 모든 데이터가 디지털 데이터로 들어오게 되고, CPU나 메모리가 처리하게 된다
* 패킷 스위칭 네트워크는 디지털 통신을 위해 사용된다
* Multiple Input이 들어오고 Output Line은 하나이다
* ***어떻게 패킷 스위칭 네트워크에서 cost-effective하고 resource sharingg하게 할 수 있을까?***
  * **By Multiplexing and Demultiplexing**

* FIFO Packet Scheduling은 VOIP를 지원하는데 충분하다
* Voice data packet은 150ms 딜레이를 넘어가면 깨질 수 있다 -> VoIP의 Qos Requirement: 150ms
---
* Latency
  * Delay = Transmission delay + Propagation delay + Queueing delay + Processing delay
  * 패킷을 잃어버린 경우. 예를 들어 카톡에서 hello라고 보냈을 때 상대방은 hello를 수신하지 못함.
  * 나는 이 패킷이 사라진지 모르고 계속 이야기 함. ACK를 받지 못했기 때문에 재전송 할지, 삭제할지 선택하라고 함.
  * **Real time Service에서 재전송은 의미가 없다** -> 갑자기 이야기하는중에 hello를 보내면 뜬금 없다

* Jitter
  * 패킷 delay의 variation을 측정한다.
  * 30ms가 넘는 Jitter는 Voice data packet에 영향을 줄 수 있다

* Packet Lost


---
* IP: Best-Effort Packet Delivery
  * 패킷 스위칭은 패킷 내부에 있는 데이터를 보낸다.
  * src & dest의 주소를 헤더에 담아서 보내게 된다. 항상 최고의 노력으로 전달하려고 하지만, 안될 수도 있다
  * 패킷을 잃어버릴 수도 있고, 패킷이 손상될 수도 있고
