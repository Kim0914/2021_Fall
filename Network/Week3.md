# IP Packet Design (9.16/9.21)

## Reliable or Unreliable in each Layer
* Application layer : ***Reliable***
* Transport Layer : TCP -> ***Reliable***, UDP -> ***unreliable***
* Network Layer : IP protocol인 경우 -> ***unreliable*** because packet will be lost, out of order, duplicated
* Data Link Layer : ***Reliable*** because of error control, flow control, congestion control
* Physical Layer : ***not reliable*** due to noises, signals will be lost corrupted
* 각각의 layer는 다른 layer가 신뢰할 수 있는지 없는지 신경쓰지 않는다 -> 자기꺼만 잘 챙기면 된다

## IP Packet format
![image](https://user-images.githubusercontent.com/68818952/134446786-f9bec180-f529-4444-914a-f2873b9959d2.png)

* Header Length
* Total length : payload + Header length
* payload length : Total length - Header length
* TTL(Time To Live) : 패킷이 무한히 살아있지 못하도록 8bit짜리 패킷의 수명을 넣는다(시간정보가 아닌, Hop 개수)
* 16-bit identification : 패킷이 도착하는 순서(정보)를 기록 => duplicate, corrupt 등 에러를 방지하기 위해
* 8-bit Protocol : 네트워크 층에서 전송 층으로 이동할 때, TCP or UDP 둘 중 어디로 갈지 정보를 담고 있음
* 16-bit Header checksum : 패킷이 하부 레이어를 통해 변조될 수 있는데 변조를 찾기 위해 checksum. header정보에 대해서만(payload X)
  * => 즉, 패킷 내부 데이터의 내용은 중요하지 않고, 제대로 전달되는지가 중요하기 때문

## Summary
1. Internet? -> **A set of different networks based on IP**
2. What is a possible architecture of the Internet -> **A network consisting of routers**
3. Possible communication layers consisting of Internet architecture -> **TCP/IP protocol suite**
4. What is minimal data unit over the Internet -> **Packet (Header + Options + Payload)**

* Communications protocol
  * 두 장치간의 통신을 하는데 있어서 필요한 규칙
* Protocol
  * 두 endpoint간에 혹은 하나의 장치 내에서 통신을 지배하는 규칙
* Architecture
  * 기능 자체의 행동과, 인터페이스, 컴포넌트간의 상호연결을 설명하는 컴포넌트를 구성하는 추상화된 시스템의 명세를 설명.

* 통신을 대표하는 2가지 프로토콜
  1. TCP 
  2. OSI

## TCP/IP Layers and Example Protocols
![image](https://user-images.githubusercontent.com/68818952/134656209-dae726c3-03b6-49de-bd67-e50600f841a8.png)
* Upper layer는 protocol 번호가 들어감. TCP는 6번
* TTL의 디폴트 값은 64이다. 하나의 Hop을 지날 떄 마다 1 감소 -> 라우터가 값을 확인하고 0이 되면 패킷을 버림
* Application layer에서 1byte의 data를 TCP로 보내는 경우 20byte + 20byte = 총 40 bytes 오버헤드 발생


## IPv6
* IOT의 개념이 등장한 가운데, 인터넷과 연결하기 위해 IP protocol을 사용 -> 모든 사물이 IP주소를 가져야 함
* 부족한 IP주소의 길이를 늘려야함 ->  모든 사물이 IP주소를 가질만큼의 IP를 할당가능
* 라우터의 주 관심사는 **빠르게 패킷을 처리** 하는 것이다.
* 라우터는 payload에는 관심없고 header에만 관심이 있다.
* 들어오는 네트워크와 나가는 네트워크의 사이즈가 다르면 framentation을 한다
* 그러나 reassemble은 하지 않는다. -> Destination의 시스템에서 파편화된 패킷을 재조립한다
* header length가 fixed이다 -> 정보를 빠르게 처리할 수 있기 때문에 H/W로 많이 쓰인다
