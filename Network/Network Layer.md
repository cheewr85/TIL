## Network Layer

## Roadmap
- [overview of network layer](#overview-of-network-layer)
- [what's inside a router](#what's-inside-a-router)
- [IP:Internet Protocol](#IP:Internet-Protocol)
- [Generalized Forward and SDN](#Generalized-Forward-and-SDN)

## overview of network layer
- network layer
	- segment를 만들어서 host에 보냄
	- 보내는 segement는 캡슐화되서 전달됨
	- network layer protocols은 모든 host, router에 존재함
	- router는 forwarding routing을 위해서 header를 가지고 있음

![one](/img/Network/Networklayer/one.png)
![two](/img/Network/Networklayer/two.png)

- Data plane
	- 데이터를 전송하는 영역, forwarding 기술, input에서 output을 어떻게 보낼지
- Control plane
	- 네트워크 전체의 로직, routing을 결정함
	- 어떻게 router를 통해서 갈 지
	- 전통적으로는 각각의 router에서 routing algorithm을 계산하였음 
	- 요즘 control plane에서는 기존의 router끼리 연결한 것을 Remote controller로 만들어 이 remote가 forwarding을 계산하여서 각각 router에 보냄

![three](/img/Network/Networklayer/three.png)
![four](/img/Network/Networklayer/four.png)

## what's inside a router
![five](/img/Network/Networklayer/five.png)

- Input port의 경우 header를 통해서 어떻게 보낼지 찾고 forwarding을 하게끔 처리를 함, 그에 맞게 datagram을 처리함

![six](/img/Network/Networklayer/six.png)
![seven](/img/Network/Networklayer/seven.png)

- 여기서 forwarding은 2가지로 나뉘어짐
	- destination-based의 경우 IP주소를 가지고 forwarding을 정함, Address 구간을 정해서 forwarding을 함, 하나하나 테이블을 만들 수 없으므로
	- 헤더 값을 이용해 forwarding 테이블을 이용해 기계적으로 router안에서 빠르게 forwarding을 할 수 있음 
	- generalized forwarding의 경우, 다른 field 값을 활용해서 정함

![eight](/img/Network/Networklayer/eight.png)

- 여기서 공통된 부분 기준으로 맞으면 Link interface를 보내는 것인데 겹치는 부분이 발생함, 이 때, longest한 것을 바탕으로 먼저 보냄

![nine](/img/Network/Networklayer/nine.png)

- Switching fabrics
	- input에서 output으로 보내느데 있어서의 타입을 이야기함, 총 3가지 타입이 있음

- 먼저 메모리 구조와 유사하게 활용하는 방식이 있음

![ten](/img/Network/Networklayer/ten.png)

- 그리고 공통 연결된 버스를 통한 처리도 존재함

![eleven](/img/Network/Networklayer/eleven.png)

- 마지막으로 링크를 만들어 엮어서 만들어 하나의 버스에 패킷이 몰리지 않게 아래와 같이 처리할 수도 있음

![twelve](/img/Network/Networklayer/twelve.png)

- input port 보다 fabric이 느리기 때문에 queueing이 발생함, 역기서 아래와 같이 데이터 처리가 되지 않은 상태에서 blocking이 발생할 수 있음

![thirteen](/img/Network/Networklayer/thirteen.png)

- 아래와 같이 output port에서 역시 이러한 queueing 문제가 발생하고 이로 인해서 loss와 delay가 생길 수 있음
- 그러므로 이러한 상황을 방지하기 위해서 scheduling을 통한 제어가 필요함

![fourteen](/img/Network/Networklayer/fourteen.png)
![fifteen](/img/Network/Networklayer/fifteen.png)
![sixteen](/img/Network/Networklayer/sixteen.png)

- 여기서 스케줄링시 링크롤 보낼 패킷처리에 있어서 아래와 같이 4가지 방법으로 처리를 할 수 있음

![seventeen](/img/Network/Networklayer/seventeen.png)
![eighteen](/img/Network/Networklayer/eighteen.png)
![nineteen](/img/Network/Networklayer/nineteen.png)
![twenty](/img/Network/Networklayer/twenty.png)

## IP:Internet Protocol
- Internet network layer는 아래와 같은 프로토콜을 활용하여 datagram packet을 파악하고 IP datagram은 아래와 같은 다양한 정보가 담겨있음

![twentyone](/img/Network/Networklayer/twentyone.png)
![twentytwo](/img/Network/Networklayer/twentytwo.png)

- 여기서 IP 전달시 아래와 같이 쪼개지고 합쳐지는 과정을 통해서 datagram을 전달함

![twentythree](/img/Network/Networklayer/twentythree.png)
![twentyfour](/img/Network/Networklayer/twentyfour.png)

- IP addressing의 경우 아래와 같이 host와 router interface를 인식하기 위한 식별자이고 아래와 같은 구조로 연결되어 있음
- 여기서 이를 연결하는 방식에 있어서 유선망인 이더넷과 wifi를 통해서 연결이 됨

![twentyfive](/img/Network/Networklayer/twentyfive.png)
![twentysix](/img/Network/Networklayer/twentysix.png)

- 여기서 아래와 같이 파란 부분으로 둘러싸여지 있는 subnet이 형성되어 있음, router없이 서로 연결된 상태임
- subnet은 아래와 같이 /의 형태에서 앞의 IP Address에서 / 이후 숫자값의 비트가 subnet port임을 의미함
- 호스트가 없어도 subnet이 가능함

![twentyseven](/img/Network/Networklayer/twentyseven.png)
![twentyeight](/img/Network/Networklayer/twentyeight.png)

- CIDR
	- 아래와 같이 위처럼 subnet으로 지정된 특정 비트에 상관없이 임의의 길이를 subnet으로 표현이 가능함
	
![twentynine](/img/Network/Networklayer/twentynine.png)