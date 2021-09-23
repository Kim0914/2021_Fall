# IP Packet Design (9.16)

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
* TTL(Time To Live) : 패킷이 무한히 살아있지 못하도록 8bit짜리 패킷의 수명을 넣는다
* 16-bit identification : 패킷이 도착하는 순서(정보)를 기록 => duplicate, corrupt 등 에러를 방지하기 위해
* 8-bit Protocol : 네트워크 층에서 전송 층으로 이동할 때, TCP or UDP 둘 중 어디로 갈지 정보를 담고 있음
* 16-bit Header checksum : 패킷이 하부 레이어를 통해 변조될 수 있는데 변조를 찾기 위해 checksum. header정보에 대해서만(payload X)
  * 즉, 패킷 내부 데이터의 내용은 중요하지 않고, 제대로 전달되는지가 중요하기 때문
