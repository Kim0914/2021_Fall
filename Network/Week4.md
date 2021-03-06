## IPV6에서 DN, ECN, Flow Level (09.23)
![image](https://user-images.githubusercontent.com/68818952/135042297-8361a9db-2eef-48a3-9f10-93f52ac8020b.png)

* 데이터가 디바이스에 도착 -> OS가 데이터를 가져와서 포트번호를 보고 프로세스에게 나눠주면 어플리케이션에서 버퍼로 만듦
* 운영체제가 바로바로 프로세스에 넘겨줄 수 없으니까 버퍼링한 다음에 넘겨줌. Send buffer, Receive buffer 유지
* 각 레이어마다 버퍼를 구성하고 있고, 라우터도 포트에 들어오는 데이터를 처리하기 위해 각각의 버퍼를 구성(queue형식)
* 패킷스위칭 기반의 네트워크는 거대한 queue들의 기반으로 이루어져있다고 생각하면 된다

* TCP Control
  1. Error Control
      * TCP segment #1을 보냈다고 하자
      * Destination은 ACK #2를 보낸다. ***"segment #1을 잘 받았고, segment #2를 받을 준비가 됐다"***
      * 여기서 ACK #1이 아닌 이유는, TCP에서는 다음 패킷을 받을 준비가 됐다는 의미도 포함되어야 하는데 ***"ACK #1은 잘 받았다"가 끝***
  2. flow Control
      * 리시버 버퍼 사이즈보다 더 많은ㄷ ㅔ이터가 들어오면 버퍼가 넘쳐난다 -> 오버플로우라고 함
      * 오버플로우를 막기 위해서 리시버는 항상 자신이 받을 수 있는 데이터량을 sender에게 알려주어야 한다
      * sender는 receiver가 받을 수 있는 양만 보내야한다.
      * flow control은 destination이 한다.
      * 그럼에도 불구하고 stable한 network가 되지 않을 수 있다. process to process간의 통신이기 때문에 라우터는 보지 않는다
      * 나를 제외하고 외부에서 패킷을 많이 보내게 되면 congestion이 발생
  3. Congestion control
      * 네트워크에 많은 양의 패킷이 도착한 경우. 사람들은 혼잡을 피하기 위해 RH를 피한다
      * **라우터가 네트워크의 혼잡을 확실하게 알 수 있다**
      * Receiver는 혼잡을 고려하지 않는다. Sender만 관여한다 -> ***네트워크 상태를 파악 후 패킷의 양을 얼마나 조절할지***
      * Sender는 어떻게 네트워크 상태를 파악할까? -> **ACK를 보내고 받은 시간을 통해(Round Trip Time)**
      * RTT는 네트워크 상태를 정확히 이야기 해주는 것은 아니다. 단지 추측을 하는 것이다

* 최신 IPv4버젼은 이러한 control들을 신경쓰지 않는다 -> unreliable 하다
* IPv6도 unreliable 하지만, 최대한 reliable하게 보내도록 한다
* IPv4와 IPv6는 **비연결성(Connection less)**이다
  * 패킷이 라우터를 통해 전달되는 방향이 계속 달라진다 -> ***패킷은 어디로 가야할지에 대한 정보를 포함해야 함***
  * **Source IP, Destination IP가 IP Header에 그래서 들어있는 것**
* 따라서 IPv6에서는 **ECN field**를 통해 congestion등이 있는지 명확하게 표현한다 (2 비트)
* Dest에서 Src로 ACK와 함께 ***"Congestion happen"*** 이런식으로 보낸다

* **DS필드는 데이터가 video, text, voice등 많은 데이터가 들어올 수 있음**
  * Packet scheduler를 통해 각 패킷을 처리할 때 마다 DS필드를 확인 후 우선순위를 보고 결정한다

* **Flow Label은 라우터가 도착한 패킷이 어디로 향할지 결졍하기 위해서는 Dest IP를 본다**
  * Desp IP를 확인하는데 시간이 걸리기 때문에, 어떤 목적지로 가는 패킷에 대해서는 각 라우터 끼리 미리 set up 한다
  * 어디로 향하는지에 따라 flow label을 작성하고, 이 flow label을 확인하여 바로바로 라우팅(보낸다) 
  * 예를들어, LG U+의 넷플릭스 서버에 접근하는 경우, 각 호스트가 보내는 패킷에다가 flow label 명시
  * 0011이라는 flow label을 라우터에 셋업해놓으면 바로바로 넷플릭스 서버로 도착함 (속도 개선)

* Transport Layer(TCP)
  * Reliable delivery of data
    * Required: error, flow control
    * Optional: congestion control
  * Ordering of delivery
  ![image](https://user-images.githubusercontent.com/68818952/135081963-57600fe9-664f-4e5f-b47a-4eb4e2ead84d.png)
  * TCP checksum은 Header와 Data 둘다 검사한다 -> Reliable하기 위해

* Applicaition Layer
  * Support for user application
    * e.g. http, SMTP(메일 전송시 사용하는 프로토콜)

* ***Network Layer가 Unreliable***하기 때문에 **Packet loss**, **Ordering of Packet**, **Packet duplication** 문제가 발생한다
* 각 라우터마다 버퍼를 유지하고 있고, 버퍼를 저장했다가 처리하기 때문에 이런 문제가 발생할 수 있다
* 라우터는 도착한 패킷의 목적지 주소를 기반으로 다음 목적지(라우터)를 결정한다

---

* **Ordering of Packet**
  * 패킷1과 패킷2가 각각 다른 라우터로 보내졌다고 하자. 패킷1이 있는 라우터가 busy해서 패킷2가 먼저 도착
  * 따라서 목적지에는 패킷1 -> 패킷2의 순서가 아닌, 패킷2 -> 패킷1의 순서로 도착하는 경우가 생긴다

* **Packet duplication**
  * Sender측에서 패킷1을 보내고 ACK를 기다리고 있는데, 패킷1이 도착한 라우터가 busy해서 ACK를 시간 내에 받지 못함
  * Sender는 패킷1을 재전송하게되면 라우터1의 queue에 패킷1이 2개가 존재하게 된다
  * 라우터1의 상태가 정상적이게 되고 데이터를 처리하게 되면 중복 

## The Definition of Hop
* One hop coverage는 무엇인가?
  * ***하나의 데이터를 보냈을 때 이 데이터를 받아볼 수 있는 범위를 One hop이라고 할 수 있다***
  * 그러나 다른 라우터는 이 데이터를 절대 받지 않는다. (라우터 <-> 라우터 개념이라고 볼 수 있다)
  * Local Area Network의 가장 큰 특성은 Broadcasting이다 -> broadcast based '***one hop-range'***
  * LAN안에서 각각의 노드들은 다른 노드의 패킷(데이터)를 들을 수 있다
