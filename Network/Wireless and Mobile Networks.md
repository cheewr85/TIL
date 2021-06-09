## Wireless and Mobile Networks

## Roadmap
- [Introduction](#Introduction)
- [Wireless links, characteristics](#Wireless-links,-characteristics)
- [IEEE 802.11 wireless LANs](#IEEE-802.11-wireless-LANs)
- [Cellular Internet access](#Cellular-Internet-access)
- [Mobility](#Mobility)

## Introduction
- wireless가 wired 사용보다 더 많음
- wireless의 두 가지 큰 특징이 존재함
	- wireless : wireless link를 통해서 통신을 함
	- mobility : mobile user가 계속 이동하면서 network 포인트가 계속해서 바뀜
- wireless network의 요소들

![one](/img/Network/Wireless/one.png)

- wireless hosts
	- 스마트폰, 노트북등의 단말기들
	- 앱을 실행하고 mobility가 있을 수 있지만 없을수도 있음, wireless라고 반드시 mobility를 갖는 것은 아니 
- base station
	- 기지국 역할, 유선과 무선 채널을 연결함
	- relay : 무선 host의 공간과 유선 네트워크 사이의 packet을 보내는 역할을 맡음, 주로 기지국과 와이파이
- wireless link
	- mobile과 base station을 연결함
	- link access를 통해서 다양한 access protocol과 연결됨
	- 다양한 data rate, transmission distance가 존재함, 감쇄가 있어서 전달에 있어서 다 다르게 받을 수 있음

![one](/img/Network/Wireless/two.png)

- Infrastructure mode
	- 기지국이 있는 모드임, 기반시설이 존재함
	- base station이 mobile과 wired network를 연결함
	- handoff(handover) : 이동을 통해서 기지국 A를 사용하다가 근처 다른 기지국 B에 가까워졌을 때 해당 기지국이 즉 base station이 바뀔 수 있음

![one](/img/Network/Wireless/three.png) 

- ad hoc mode
	- base station이 존재하지 않음, 각각 영역끼리 연결하고 본인들끼리 연결함
	- 각각 노드들은 link coverage안에 있는 다른 노드에게만 전송할 수 있음
	- 노드들이 그들 스스로 네트워크를 구성함

![one](/img/Network/Wireless/four.png) 

## Wireless links, characteristics
- wired link와는 다른 특징들이 존재함
- decreased signal strength
	- 무선으로 보내는 것이기 때문에 감쇄가 심하게 나타남, path loss -> 1,2m가 지남에 따라 손실이 계속해서 일어남
- interference from other sources
	- 정규화된 무선 네트워크 frequency가 다른 디바이스와 공유됨, 이로 인해서 전파 사용자들 사이에서 간섭이 일어남
- multipath propagation
	- 신호가 반사가 되면서 기존에 정상적으로 보낸 신호와는 다르게 도착함, 신호 모두가 도착시간이 다 다름, multipath를 만들어냄
- 이러한 특징들로 인해서 wireless link가 더 어려움
- SNR : signal-to-noise ratio
	- larger SNR은 noise로부터 signal을 추출하기 쉬워짐

![one](/img/Network/Wireless/five.png) 

- 많은 wireless senders와 receivers로 인해서 아래와 같은 문제가 생길 수 있음

![one](/img/Network/Wireless/six.png) 

- Code Division Multiple Access(CDMA)
	- 각각 유저에게 특정 code를 할당 시킴
	- 모든 유저는 같은 주파수를 가지고 있으나 encode시 각각 유저들은 그들만의 sequence를 가지고 있음
	- 코드들은 서로 orthogoanl하기 때문에 간섭이 최소화로 일어남
	- encoded signal = original data x chipping sequence
	- decoding은 encoded signal과 chipping sequence의 inner-product임

![one](/img/Network/Wireless/seven.png)
![one](/img/Network/Wireless/eight.png)

- 위의 예시처럼 encode를 처리한 뒤 receiver 부분에서 received input과 code를 inner-product하여서 channel output을 구함

## IEEE 802.11 wireless LANs
![one](/img/Network/Wireless/nine.png)

- 위와 같이 Wifi는 구성되어 왔음

![one](/img/Network/Wireless/ten.png)

- wireless host는 base station을 통해서 Internet과 소통함
- base station은 access point(AP)임, 공유기들을 나타냄
- BSS(Basic Service Set)에서는 wireless hosts, access point(AP) ad hoc mode가 포함됨, 위의 나온 그림처럼

- 802.11 Channels, association
	- 2.4GHz등 주파수와 주파수에 따른 채널이 존재함
	- AP마다 다름, 왜냐하면 같은 주파수 대역을 모두 다 사용하게 되버리면 간섭이 발생하기 때문에 이를 줄이기 위해서
- host는 반드시 AP와 연결되어야 함
	- 이를 위해서 channel을 스캔하고 beacon을 통해서 AP의 정보를 알려줌
	- AP가 이를 바탕으로 인식을 하고 Wifi가 검색시 나타남
	- 그리고 인증을 한 뒤 Subnet IP 주소가 할당됨, AP를 통해서

![one](/img/Network/Wireless/eleven.png)

- 위와 같이 스캔을 할 때 pasive, active하게 스캔을 하여서 Wifi의 연결을 함
- 여기서 Wifi에서 multiple access가 일어날때 즉 2개 이상의 노드가 동시에 전송을 할 때
	- CSMA 전송하기 전에 실행함
	- 충돌 탐지를 하기 힘듬, 무선통신이므로 신호를 보낼때 감쇄가 많이 일어나므로 충돌에 대해서 정확히 탐지하기 힘듬
	- fading과 hidden node problem을 통해서 충돌이 발생
	- 이를 피하기 위해서 CSMA/CA(Collision Avoidance), 최대한 collision이 안나게 하기 위해서 씀
- CSMA/CA

![one](/img/Network/Wireless/twelve.png)

- 충돌 방지를 위해서 위와 같이 CSMA/CA를 활용함
- 먼저 sender에서 DIFS 즉 사용전에 기다림, 만일 사용중이 아니면 data를 보냄
- 만일 채널에 사용중이면 random backoff time을 시작하고 timer가 채널을 쓸 수 있을 때까지 카운트다운함
- 만일 ACK이 제대로 오지 않았다면 random backoff interval을 증가시킴
- reciver에서는 SIFS이후 ACK을 보냄

- Avoiding Collision
	- hidden node problem의 문제로 인해서 AP에서 확실하게 그 node 사이에서 데이터를 못 받고 서로 충돌이 일어나는 상황을 알릴 수 없음, 서로 노드가 충돌되는것을 서로 다른 노드가 인지하지 못하므로
	- 그래서 RTS를 서로 보내다가 충돌이 일어날 수 있음, 이때 두 노드 중 한 노드가 RTS를 먼저 보냄
	- 그러면 AP에서 두 노드에게 CTS를 보냄, 그러면 CTS가 모든 노드들이 듣기 떄문에 충돌이 일어나게끔 노드를 보내는 상황이 일어나지 않음

![one](/img/Network/Wireless/thirteen.png)

## Cellular Internet access
- 우리가 흔히 쓰고 있는 이동통신 네트워크를 가르킴
- cell은 아래와 같이 구성되어 있고 지리적으로 해당 범위까지를 커버함
- air-interface는 물리적으로 통신하는 과정을 의미함
- MSC를 통해서 현재 있는 cell에서 벗어나서 움직였을 때 그 벗어난 것을 기점으로 근처의 다른 cell에 연결을 해 줌, 이동성 보장을 위해

![one](/img/Network/Wireless/fourteen.png)

- 앞서 배운 FDMA와 TDMA의 기술이 합쳐져서 사용됨, 시간과 주파수 둘 다 쪼개서 활용함

![one](/img/Network/Wireless/fifteen.png)

- 2G는 아래와 같은 구조를 가지고 있었음, Gateway를 통해서 외부로 들어가고 나가는 것을 총괄함, 이때는 인터넷 통신은 필요하지 않았음

![one](/img/Network/Wireless/sixteen.png)

- 3G 구조는 아래와 같음, 기존의 2G 전화통화 구조에서 인터넷 연결을 추가함, data에 연결함
- 기존 2G 구조에서 병렬적으로 data network가 연결됨, 인터넷 연결 위해서 SGSN, GGSN이 추가됨

![one](/img/Network/Wireless/seventeen.png)

- core network에서 전화, 인터넷, 과금등의 연결을 체크함
- radio access network(RAN)에서는 무선 access, 실제 데이터를 받아옴

![one](/img/Network/Wireless/eighteen.png)

- 4G의 경우는 모든걸 IP 기반으로 처리함, 인터넷만, 그래서 기존에 있던 전화에 대한 연결은 없음, 전화의 경우 VoIP, 즉 데이터 기반으로 함
- MME, HSS등을 통해서 통신사등의 가입여부 확인함, S-GW, P-GW를 통해서 data가 드나듬

![one](/img/Network/Wireless/nineteen.png)

- IP 기반으로 통신하기 때문에 앞서 배웠던 layer 구조를 활용한 캡슐화를 해서 데이터를 보내는것과 tunneling을 통해 통신하는 것, 역시 유사하게 처리하게 됨

![one](/img/Network/Wireless/twenty.png)
![one](/img/Network/Wireless/twentyone.png)

## Mobility
- mobility가 있다는 것은 아래와 같이 구분할 수 있음

![one](/img/Network/Wireless/twentytwo.png)

- Mobility를 이해하기 이전에 아래와 같은 구조로 되어 있음을 알아야 함
	- home network에 경우 기존에 쓰는 영구적인 곳임, 영구적으로 할당 받은 address가 있고 home agent를 통해서 기존에 사용하는 곳이 있다면 쓰이게 됨
	- 여기서 만일 다른 곳으로 이동을 했을 때 permanent address의 경우는 가지고 있지만 home이 아니기 때문에 별도로 접속이 됨
	- 그래서 여기서 임시로 방문한 곳에 대해서 care-of-address를 할당 받고 visited network를 사용하면서 foreign agent가 통제를 함
	- 여기서 correspondent 이 mobile과 통신하고자 할 때 correspondent는 home network밖에 모름, 즉 위치가 바뀌면 그에 맞춰서 visited network에 접속하는 것이 아닌 home network에 접속하려고 하는 것임

![one](/img/Network/Wireless/twentythree.png)
![one](/img/Network/Wireless/twentyfour.png)

- 여기서 생각할 부분이 그럼 이런식으로 address가 바뀔 경우 어떻게 찾아야 할 지 고민해봐야함
- 만일 이를 router를 통해서 table이 바뀔 때마다 체크를 하게 한다면 바뀔 때마다 모든 table을 보내고 수많은 모바일기기를 통제해야 하기 때문에 모든걸 다 해 줄 수 없음
- 이를 해결하기 위해서 end-systems이 이를 통제함
	- indirect routing : home agent를 통해서 correspondent로부터 mobile과 통신을 함, remote로 forward를 함
	- direct routing : correspondent가 mobile의 foreign address를 알게 되고, mobile에 direct로 보냄
- 아래와 같이 wide area network에서 foreign agent와 home agent가 각각 서로의 상태를 알고 있음

![one](/img/Network/Wireless/twentyfive.png)

- Mobility via indirect routing
![one](/img/Network/Wireless/twentysix.png)

- correspondent가 먼저 접속하기 위해서 home mobile에 먼저 접속함
- 그 다음 home agent가 home mobile에 접속한 correspondent를 intercept한 후 wide area network를 통해서 foreign agent로 forwarding을 함
- 그럼 foreign agent가 forwarding한 것을 받음
- 그리고 받은 것을 foreign이 correspondent에게 visited network에 있는 접속하기 위한 mobile을 알려줘서 보냄

![one](/img/Network/Wireless/twentyseven.png)
![one](/img/Network/Wireless/twentyeight.png)

- Mobility via direct routing
![one](/img/Network/Wireless/twentynine.png)

- direct의 경우 forwarding이나 wide area를 사용하는 것이 아니라 home network를 통해서 foreign mobile에 대한 정보를 직접 correspondent가 받음
- 그래서 이를 통해서 직접 foreign agent에 통신을 함

![one](/img/Network/Wireless/thirty.png)
