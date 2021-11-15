## NAT and TCP ports
* 대부분의 IP 패킷은 TCP나 UDP payload를 사용한다.
  * TCP UDP 둘 다 헤더에 src port, dest port 정보를 담고있다
* 우리는 TCP를 다룰 것이다. -> UDP도 동일하게 동작한다
* port는 16비트로 나타내고, process to process delivery를 하기 위해서 사용한다.

![11-NAT-Secured-7](https://user-images.githubusercontent.com/68818952/141796543-b9ca7ad3-e96d-4d66-a4e6-7da8cdac7e79.jpg)
![11-NAT-Secured-8](https://user-images.githubusercontent.com/68818952/141796556-1249a105-2f2f-42a5-a8bb-6b533370871c.jpg)
![11-NAT-Secured-9](https://user-images.githubusercontent.com/68818952/141796576-8d4c61ac-15aa-452b-8bd6-9a74a57d93e1.jpg)

1. 톰의 집에 폰과 노트북 두 개의 device가 있다.
2. 톰이 폰이나 노트북을 이용하여 네이버에 접근하려고 한다.
3. 톰 집의 port number는 2000 이라고 하자. 패킷을 보내기 위해 port #를 사용한다.
4. 톰이 폰과 노트북 둘 다 네이버로 접속하려고 할 때 패킷을 전송하는데 반드시 두 장치를 구분해야 한다.
5. 톰의 집(AP)를 지나 public network 51.22.33.44를 타고 네이버로 접속한다.
6. 네이버 입장에서 response를 할 때, 51.22.33.44의 주소만 가지고는 폰, 노트북을 구분할 수 없다.
7. 따라서 NAT 테이블을 관리한다 !
8. NAT 테이블에서 origin src port, origiin dest port, src ip, dest ip 정보를 유지한다
9. 이 정보들은 테이블의 key로 구분된다. key가 5000인 레코드의 정보, key가 5001인 레코드의 정보
10. 패킷들이 NAT 테이블에 도착하면 Dest port#를 참조해서 패킷을 수정하여 forward 한다.

## NAT
* Source port field를 사용해서 문제를 해결할 수 있었다.
* Private IP addresses <-> ISP addresses (Internet Servie Provider)
* 앞서 NAT 예시를 정리해보면,
  * **1. 사설 IP 에서 밖으로 나가는 패킷이 NAT 박스를 만나면, 192.168.xx.xx -> public IP로 바뀌게 된다**
  * **2. NAT 테이블의 Key value가 패킷에서 TCP source port 정보에 들어간다. (약 65,536개의 key)**
  * **3. IP, TCP 헤더 checksum들은 변형된(수정된) 패킷 정보를 가지고 있다**
  * **4. 패킷이 ISP로 부터 NAT box에 도착하면, TCP 헤더의 Source port를 보고 NAT Table Index에서 찾은 후 Source port를 변경한다**
  * **5. 내부 IP 주소와 original TCP source port가 패킷에 다시 들어온다**
  * **6. IP, TCP 헤더 checksum들은 재조립된다.**
  * **7. 패킷이 company router를 지나가게 되고 자신의 목적지(폰, 노트북)으로 찾아간다**
