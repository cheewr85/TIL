## The Link Layer and LANs

## Roadmap
- [Introduction](#Introduction)
- [Error detection](#Error-detection)
- [Multiple access protocol](#Multiple-access-protocol)

## Introduction
- Link layer에서는 hosts와 routers에 대해서 링크로 연결되는 것들로 nodes라고 부름
- 이러한 인접한 노드들을 연결하여서 데이터들이 점대점으로 전송될 수 있도록 links로 연결함
- 이러한 데이터를 캡슐화하여서 frame으로 만들어서 전송하고 보냄
- 한 번 이런식의 데이터가 주고 받을 때 점대점 방식으로 매우 많이 전송이 오고 가게됨
- 그리고 아래와 같은 특징을 지님

![one](/img/Network/Linklayer/one.png)

- 이러한 link layer는 모든 host들에 적용이 되는데 여기서 이 host에 적용될 때 아래와 같이 물리적인 hardware를 매개하여서 사용이 됨
- 여전히 이러한 부분의 칩셋은 존재를 함
- 그 중 대표적인 것이 adaptor인데 아래와 같이 datagram을 보내는데 있어서 전송과 수신 그리고 이를 캡슐화해서 보내는데 역할을 함

![one](/img/Network/Linklayer/two.png)
![one](/img/Network/Linklayer/three.png)

## Error detection
- Error detection의 경우 여기서 link layer로 보낼때 단순히 데이터만을 보내진 않음
- 추가적으로 에러 발생을 확인하고 수정하기 위한 데이터를 덧붙여서 보냄
- 그리고 만일 그 field에서 error가 없다면 그대로 데이터를 보내면 되고 error가 있다면 그걸 체크하고 수정하는 과정으로써 사용하면 됨

![one](/img/Network/Linklayer/four.png)

- 가장 기초적인 방식이 parity checking임
- 실제 보내는 bit에 parity bit을 덧붙여서 보냄, 여기서 parity bit은 해당 data를 기준으로 1의 개수를 홀수개인지 짝수개인지 기준을 정하고 그 기준에 맞게 partity bit을 설정하는 것임
- 여기서 만약 기준을 짝수개로 정했어서 parity bit을 그에 맞춰서 설정하였는데 만일 검출시 홀수개로 나온다면 error가 발생한 것임
- 하지만 에러가 2개나면 검출하기 힘듬, 그러므로 매우 신뢰도가 높아 에러가 날 확률이 적을 때에만 사용함

![one](/img/Network/Linklayer/five.png)

- Internet checksum은 앞서 배운바와 같이 segment contents에 대해서 추가적으로 활용하여 checksum 값을 직접 다 확인하여 그 field가 맞는지 계산하여서 체크하는 과정임
- 그 외에 추가적으로 강력한 error detection으로 Cyclic redundancy check이 있음
- 여기서 D라는 data bit에서 r+1의 bit pattern으로 G를 선택하고 최종적으로 CRC bits인 R을 선택하여 D,R에서 G로 나누는것임
- 여기서 G로 나눌때 나누어 떨어진다면 에러가 없는것이고 나누어 떨어지지 않으면 에러가 있는것임 
- 이는 r+1 이상의 비트를 보내게 된다면 에러 검출이 힘들 수 있음
- 아래와 같은 로직으로 구성되어 있고 계산을 할 수 있음

![one](/img/Network/Linklayer/six.png)
![one](/img/Network/Linklayer/seven.png)

## Multiple access protocol
- link는 point-to-point, broadcast로 나뉘어짐
- 여기서 Multiple access links, protocols은 주로 broadcast에서 많이 이루어짐

![one](/img/Network/Linklayer/eight.png)

- 하나의 공유된 broadcast channel을 가지고 있음
- 2개 그 이상의 노드들이 동시에 전송을 할 경우 간섭이 생김, 만일 여기서 동시에 하나 이상의 신호를 보내면 충돌이 일어남
- 이를 조절하고 해결하기 위해서 multiple access protocol을 활용함
- 분산 알고리즘을 통해서 공유된 채널에 대해서 node들이 어떻게 전송을 할 지 정해줌
- 해당 channel 역시 그 channel 자체로 통신을 해야함, 즉 무선채널로 통신하는데 유선채널에 대한 access를 요구하고 확인할 수 없음
- 이상적인 상태로는 아래와 같음

![one](/img/Network/Linklayer/nine.png)

- MAC protocols
	- channel partitioning
		- channel을 작은 pieces로 쪼개서 나눔
		- time slot, frequency, code를 통해서 나눔
	- random access
		- channel이 쪼개져있지 않음, 랜덤하게 접속함, 충돌이 일어남
		- 이 충돌에서 recover를 함
	- taking turns
		- token을 통해 처리, 즉 순서를 전해서 진행을 함

- Channel partitioing TDMA
	- time division multiple access
		- rounds를 통해 channel에 접속함
		- 각 round를 시간을 통해서 노드들을 나눠서 쪼갬
		- 사용하지 않은 slot은 비어 있음

![one](/img/Network/Linklayer/ten.png)

- Channel partitioning FDMA
	- frequency division multiple access
		- channel spectrum이 frequency bands에 맞게 나뉘어짐
		- 각각 station이 frequency band에 할당됨, 주파수를 쪼개 각각 대역을 나눈 뒤 노드에 할당함
		- 사용되지 않는 시간에는 비어있음
	- 추가적으로 CDMA, 즉 code를 통해서 나누는 경우도 있었음, 주로 3G 등 사용시

![one](/img/Network/Linklayer/eleven.png)

- Random access protocols
	- 원래는 Wifi에 주로 사용하기 위해서 만듬
	- 노드가 packet을 보낼 대 full channel data rate R을 씀, 다른 노드에 상태를 고려하지 않고 일단 랜덤하게 보냄
	- 2개 이상의 노드를 보낼 때 충돌이 일어남
	- 그러므로 충돌을 탐지하고, 충돌로부터 recover하기 위한 protocol의 사용이 필요함
	- slotted ALOHA, ALOHA, CSMA, CSMA/CD, CSMA/CA 등이 있음

- Slotted ALOHA
	- 모든 frame 사이즈가 동일하고 동일한 slot으로 시간이 나뉘어짐
	- slot이 시작할 때 노드가 보내지고 노드는 보내질때 시간이 동기화됨
	- 충돌이 발생시 모든 노드들이 충돌을 감지함을 가정하고 작동함
	- 노드가 새로운 frame에서 다음 slot으로 보낼 때
		- 충돌이 없다면 새로운 frame의 slot에 보낼 수 있음
		- 충돌이 발생하면, p의 확률로 성공할 때까지 재전송을 함, 고려를 하지 않고 계속 바로바로 보내면 충돌만 계속 일어나므로
	- 아래와 같이 장단점과, 해당 효율을 계산할 수 있음

![one](/img/Network/Linklayer/twelve.png)
![one](/img/Network/Linklayer/thirteen.png)
