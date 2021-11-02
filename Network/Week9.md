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
