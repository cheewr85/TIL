## Wireless and Mobile Networks

## Roadmap
- [Introduction](#Introduction)
- [Wireless links, characteristics](#Wireless-links,-characteristics)


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