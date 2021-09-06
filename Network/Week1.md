# 컴퓨터 네트워크에 대한 개념
* 컴퓨터는 cpu, 메모리를 가지고 있고 디지털 정보를 처리하기 때문에 컴퓨터 네트워크는 결국 디지털 네트워크를 의미한다

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


## 4. Minimal data unit over the Internet
