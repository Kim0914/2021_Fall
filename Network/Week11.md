## Internetworking Fundamental Concept of IP Address
* IP 주소 구조는 계층적이다 -> 네트워크 부분, 호스트 부분으로 나눌 수 있다.
* 192.128.15.25 이런 숫자의 IP는 Human readable, 컴퓨터는 C0290614 처럼 이진수로 읽는다
* Netmask: 255.255.255.0
* IP 주소는 범위에 따라 class를 가진다
  * Class A: 0.0.0.0 ~ 127.255.255.255
  * Class B: 128.0.0.0 ~ 191.255.255.255
  * Class C: 192.0.0.0 ~ 239.255.255.255
  * Class D: 244.0.0.0 ~ 239.255.255.255
  * Class E: 240.0.0.0 ~ 255.255.255.255
  * Class A ~ C는 Unicast, Class D는 Multicast, Class E는 Reserved for Future
* 127.xx.yy.zz는 client - server 구조에서 하나의 머신에서 테스트 할 때 사용하는 loopback address이다.
