# Conception of Computer Network
* 네트워크는 **노드**와 **링크**로 구성되어 있는 것
* 그래프의 정의와 비슷하다고 생각하면 된다. 여러개의 vertex와 edge로 연결 되어있는 상태
* 네트워크에서는 vertex 대신 node라는 개념을 쓰고, edge 대신 link 라는 개념을 쓴다
* 컴퓨터는 cpu, 메모리를 가지고 있고 디지털 정보를 처리하기 때문에 컴퓨터 네트워크는 결국 디지털 네트워크를 의미한다
* Packet Switching 의 주요 개념은 Store and forward (저장하고 보내기)

## 1. What is internet?
* Internet is a set of networking using **IP Protocol(some standard rules)**
* Protocol is RULE.
* Internet -> to exchange data -> set standardized rules -> the name these rules -> IP Protocol
* ***Interconnected computer networks*** that transmit data by some communication technologies using standard Internet Protocol
* ***network of network***

## 2. Architecture of the Internet
* consist of hosts and routers
* node를 세분화 하면 2가지로 나눌 수 있는데, end-node와 switching-node로 나눌 수 있다. 
* Host : end-node, Router : switching-node
* 라우터 밑에 여러개의 엔드 노드가 있다
* Link, host, Router로 Internet Architecture가 이루어져 있다.


## 3. Possible communication layers
* TCP/IP protocol stacks(suite) have 5 layers
  * Application
  * Transport
  * Network
  * Data Link
  * Physical


![image](https://user-images.githubusercontent.com/68818952/132167524-97b2127d-5cb7-49c5-bff7-3bd10f35d5df.png)
* each layer => each protocal
* Why Layer? in the computer network


![image](https://user-images.githubusercontent.com/68818952/132171071-07c4c2d0-cee9-41cd-ae52-dbd786442ba8.png)

* host와 host 사이에는 5 Layers로 구성되어 있는데, Router는 3 Layers로 구성되어 있는 이유가 무엇일까?
* 계층(Layer)가 왜 필요할까?



### User A , User B Data Transmission example
![image](https://user-images.githubusercontent.com/68818952/132323077-c71e5177-dd49-4763-aac5-b4f86e923ec4.png)

* **User A**가 소프트웨어(ex. 카카오톡) 에서 message를 작성
* 프로세스에서 메세지를 보내기 위한 프로토콜(상대방의 어떤 프로세스에 접근해야하는가)에 따른 메세지 포맷 생성
* 즉 각 프로세스 마다 운영체제로 부터 **Port Number**를 할당 받는다.
* Port Number는 편지를 주고 받는 과정에서 보내는 사람, 받는 사람의 이름과 같은 역할
* ***SRC, Dest, Port 1, Port 2, message*** 의 형식으로 패킷을 만든다. 이 형식에서의 각각의 정보는 절대 바뀌지 않는다
* **User B**는 전달된 데이터에서 본인의 IP와 맞는지 확인한 후, User B의 프로세스에게 Port Number를 전달한다
* **User B**의 Process는 사용자에게 메세지를 전달한다


![image](https://user-images.githubusercontent.com/68818952/132320961-615aac17-a850-418b-bece-3c0271a17aab.png)

* User A 와 User B 사이의 거리가 먼 경우 중간 매체가 필요함
* 중간 매체(ex.라우터)와 User들 간의 통신도 필요하다
* 위에서 언급했던 패킷에 각각 해당하는 MAC 주소를 SRC, Dest 형태로 덧붙힌다
* ***MAC1, MAC2, SRC, Dest, Port 1, Port 2, message*** MAC1, MAC2는 서로 통신하는 두 매체간의 주소를 의미한다
*  ***SRC, Dest, Port 1, Port 2, message*** 부분의 정보는 절대 변하지 않으며, MAC값만 변경된다




