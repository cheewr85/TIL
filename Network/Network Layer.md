## Network Layer

## Roadmap
- [overview of network layer](#overview-of-network-layer)
- [what is inside a router](#what-is-inside-a-router)
- [IP Internet Protocol](#IP-Internet-Protocol)
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

## what is inside a router
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

## IP Internet Protocol
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

- CIDR(Classless Inter Domain Routing)
	- 아래와 같이 위처럼 subnet으로 지정된 특정 비트에 상관없이 임의의 길이를 subnet으로 표현이 가능함
	
![twentynine](/img/Network/Networklayer/twentynine.png)

- DHCP(Dynamic Host Configuration Protocol)
	- plug-and-play, IP 주소를 자동으로 할당해주는 방식임
	- 동적으로 IP 주소를 얻어, IP주소를 host가 얻을수 있게 해줌
	- 아래와 같은 구조를 가지면서 아래와 같은 일련의 처리 과정을 거침
	- IP 할당 뿐 아니라 network에 대한 정보 또한 알 수 있음

![thirty](/img/Network/Networklayer/thirty.png)
![thirtyone](/img/Network/Networklayer/thirtyone.png)
![thirtytwo](/img/Network/Networklayer/thirtytwo.png)
![thirtythree](/img/Network/Networklayer/thirtythree.png)

- DHCP의 실제 과정은 아래와 같이 됨

![thirtyfour](/img/Network/Networklayer/thirtyfour.png)
![thirtyfive](/img/Network/Networklayer/thirtyfive.png)
![thirtysix](/img/Network/Networklayer/thirtysix.png)

- 여기서 단순히 local에서, 집에서 쓰는 것이 아닌 기관에서 사용은 좀 다름
- 아래와 같이 ISP blocks을 통해서 기관들의 IP를 할당함
- subnet mask를 활용해 기관들에게 ISP blocks를 바탕으로 block화 시켜서 씀

![thirtyseven](/img/Network/Networklayer/thirtyseven.png)

- 이를 계층화시켜서 관리함

![thirtyeight](/img/Network/Networklayer/thirtyeight.png)
![thirtynine](/img/Network/Networklayer/thirtynine.png)

- NAT(Network Address translation)
	- Internet 상에서는 같은 IP Address이지만 router를 통해서 실제 local network에서 각자 사용시 서로 다른 IP Address임
	- 이처럼 하나의 IP를 가지고 여러 local network가 쓸 수 있게 하는 것이 NAT임
	- 이를 활용하면 local에서 다양한 기기들이 NAT 바탕으로 하나의 IP Address를 받은 것을 바탕으로 쓸 수 있음, 아래와 같은 구조임

![fourty](/img/Network/Networklayer/fourty.png)

- 이 과정은 아래와 같이 각각의 local IP Address를 NAT을 통해서 사용할 경우 translation table을 통해 해당 Address를 기억하고 그 전에 외부 IP로 바꾼뒤 기존 IP 역시 기억하고 그 다음 해당 IP를 받고 기억한 translation table을 바탕으로 다시 보내는 과정으로 진행됨

![fourtyone](/img/Network/Networklayer/fourtyone.png)

- IPv6
	- IPv4의 주소 부족 문제로 생긴 기술
	- header format이 processing과 forwarding을 함, 여기서 QoS를 통해서 바뀜 
	- header length가 40 byte로 fixed 되어 있고 fragmentation을 허용하지 않음
	- 이외에도 아래와 같이 checksum과 ICMPv6 등의 변화가 있음

![fourtytwo](/img/Network/Networklayer/fourtytwo.png)
![fourtythree](/img/Network/Networklayer/fourtythree.png)

- 여기서 IPv6가 생겼지만 기존에 있던 모든 IPv4를 동시에 대체할 수 없음, 불가능함
- 그래서 이를 극복하기 위해서 Tunneling을 활용하여서 기존 IPv4를 활용해서 사용함
- 이는 IPv4 datagram에 IPv6를 집어넣는 형태로 아래와 같이 사용함


![fourtyfour](/img/Network/Networklayer/fourtyfour.png)
![fourtyfive](/img/Network/Networklayer/fourtyfive.png)