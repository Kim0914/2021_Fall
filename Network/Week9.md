## Alternative to RARP (BOOTP)
* RARP를 구현하기 어렵다는 단점이 있어 이를 대체하는 것으로 **BOOTP**가 등장했다.
* BOOTP는 메세지를 전달하기 위해 **UDP/IP 패킷을 사용**한다.
* Dest IP에 255.255.255.255를 담아서 보낸다.
* 하부 레이어에서 FFFFFF라고 MAC 주소를 채워서 보낸다.
* **라우터는 기본적으로 255.255.255.255 패킷은 절대 forward 하지 않는다**
  * 라우터의 세팅값을 바꾸게 되면 할 수는 있다.
  * Limited Broadcast라고 한다 !
  * BOOTP 서버는 반드시 해당 시스템 LAN 내에서만 반응한다.
* BOOTP는 동적 주소 할당을 제공하지 않는다.

## DHCP 
* RARP -> BOOTP -> DHCP의 순서로 진화했고 BOOTP의 확장 버젼이다.
* * 무선 네트워크 환경에서는 수 많은 디바이스가 AP에 접근했다가 나갔다 하는데 이 장치에 대한 모든 MAC주소를 할당하는 것이 힘들다
  * 따라서 동적 할당이 필요해졌다.
* DHCP서버는 pool of available IP's for use on demand를 유지하고 있다.
* 다른 네트워크에 DHCP서버를 유지하고 싶으면 **relay agent**를 사용하면 된다.
![image](https://user-images.githubusercontent.com/68818952/139782292-aadf1bc2-b0f2-4d38-ae3c-127d089af9a6.png)

* DHCP 서버는 6개의 step으로 유지된다. **Client의 상태를 계속 체크해야한다 why? IP를 회수해야하기 때문에**
  * INITIALIZE
  * SELECT
  * REQUEST
  * BOUND
  * RENEW
* DHCP Packet exchange
  * DHCP Discover **Client to AP** (IP broadcast 255.255.255.255)
  * DHCP Offer
  * DHCP Request
  * DHCP ACK

## Measurement
* Network performance Metrics: **Bandwidth, Latency**
1. Bandwidth: **Data Transmitted per time unit **
2. Throughput: **The number of completed Jobs(Task, bytes, packets, bits) / Observed Time** 
3. Utilization: 
4. Latency(Delay): Queueing Time + Transmission Time + Propagation Time

* Bandwidth와 Throughput이 같다고 할 수 있을까?
  * 아님. Why? **밴드위스는 단지 시간당 데이터 전송률을 나타낸다. 이 데이터는 성공하든 실패하든 상관없음.**
  * **Throughput은 전송에 성공한 데이터**만 다룬다

* Utilization이 Throughput과 같다고 할 수 있을까?
  * 아님. Why? measurement unit이 다름. Utilization은 time/time (no measurement unit, Only scalar value) Throughput은 bit,packet/sec
  * Utilizationdptj Busy time이 number of completed job을 의미하지 않음.


## NAT(Network Address Translation)
* IOT는 컴퓨터 네트워크에서 매우 유명한 것이다. 각각의 사물들은 IP 주소를 가지고 있다.
* IPv4는 32bits이고 가능한 IP의 수는 2^32개 이므로 IP를 할당하기에 충분하지 않다.
* 그 대안으로 IPv6를 사용하자는 방법이 나왔지만 trnasition이 매우 느리다
* 그래서 NAT가 등장했다.

## NAT Box and Private IP Address
* IPv4에는 Broadcast, Multicast, Unicast 방식이 있다
  * 브로드캐스트는 시스템의 모든 구성원에게 알리는 방식
  * 멀티캐스트는 시스템의 특정 구성원에게 알리는 방식
  * 유니캐스트는 시스템의 특정 한 사람에게 알리는 방식
* Public IP vs Private IP
  * Public IP는 open to world, unique하다. 
  * Private IP는 not open to world. 정해진 구역 내에서만 사용가능하다. 시스템 밖에서는 접근할 수 없다(패킷 전송 X)
    * 10.0.0.0 ~ 10.255.255.255 는 주로 회사나 대학교에서 사용되는 Private IP이다
    * 192.168.0.0 ~ 192.168.255.255 는 가정이나 작은 사무실에서 사용되는 Private IP이다 
![image](https://user-images.githubusercontent.com/68818952/139827071-8911a6d8-edb7-4239-886e-53389a828f8a.png)
* 서로 다른 사설망에서 192.168.0.2라는 주소를 가질 수 있다.
* 한 시스템이 192.168.0.2에게 패킷을 보내려고 하면 라우터는 어떤 192.168.0.2로 보내야 하는지 모른다
* 따라서 **라우터는 Private IP를 버린다 => 이것이 문제다** 

---
![image](https://user-images.githubusercontent.com/68818952/139829341-bad0488d-a96e-4033-a1c1-daa2ea6c43be.png)
* 톰의 집에서 192.168.0.2 라는 시스템이, 네이버 웹서버 51.36.12.34로 패킷을 보내고 싶을 때
* SRC에는 192.168.0.2, Dest에는 51.36.12.34로 담아서 패킷을 보내게 된다.
* 이후 **톰의 집 AP를 지나 라우터의 다른 이더넷 칩셋을 Public IP로 통과하게 되면**
* **SRC에는 164.125.37.88(Public IP)**, **Dest에는 51.36.12.34**로 담겨서 전송된다.
* 네이버 웹서버에서 패킷을 받고, 다시 톰에게 보내야 된다.
* 이때 **SRC에는 51.36.12.34, Dest에는 164.125.37.88(192.168.0.2이 아님)을 담아서 보낸다**.
  * 왜냐하면 네이버 웹서버와 연결된 라우터에서 Dest에 Private IP가 담긴 것을 보고 패킷을 drop하기 때문에.
* 이 **패킷이 톰의 AP에 도달하게 되면 NAT를 이용해 SRC에 51.36.12.34 Dest에 192.168.0.2**로 패킷을 담아 보낸다

## Question
![image](https://user-images.githubusercontent.com/68818952/139830630-d2fbb1b0-5918-435f-b8a4-45bf946e303d.png)
* 만약 위와 같은 상황에서, 192.168.0.2 와 192.168.0.3이 똑같이 네이버 웹서버로 패킷을 보낸다고 하면
* 톰의 집 AP를 통과한 이후에는 같은 형태의 패킷이 될 것이다.
* SRC: 164.125.37.88 Dest:51.36.12.34
* 그럼 이 두 패킷을 어떻게 구분해야 할까?
* 따라서 Private IP만으로는 부족하고 또 다른 정보가 필요하다 !!

