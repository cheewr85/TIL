## Introduction

## Roadmap
- [what is the internet?](#what-is-the-internet?)
- [network edge](#network-edge)
- [network core](#network-core)
- [delay, loss, throughput in networks](#delay-loss-throughput-in-network)
- [protocol layers, service models](#protocol-layers-service-models)
- [networks under attack:security](#networks-under-attack-security)
- [history](#history)

## what is the internet?
![one](/img/Network/Introduction/one.png)

- PC,laptop,smartphone,notebook 우리가 사용하는 기기들 + 서버
- 서버에 있는 동영상을 우리가 사용하고 기기들을 통해서 보는 것, 그런 인터넷 환경을 즐기고 있음
- 서버 <-> 스마트폰 서로 연결되어 있음(수십억개)
- 우리가 사용하고 있는 기기의 말단, 그리고 받는 서버의 말단을 host(end systems)라고 함
- 실제 실행하는 것

- 통신링크
	- 두 장치를 연결시켜주는 통신을 위한 연결을 의미함
	- 다양한 매개체를 통해 장치를 연결할 수 있음, 링크별로 대역폭이 정해져 있음 
	- 무선 유선으로 링크를 연결할 수 있음
- 유선링크(랜선)
	- 라디오 전파를 통해서 전파 연결 가능, 구리 & 광섬유 등으로 전파 연결 가능 
- transmission rate(전송률, 업로드 속도, 다운로드 속도) -> bandwidth(대역폭)

- 패킷 스위치(라우터)
	- 인터넷을 통해 데이터를 주고 받을 때 패킷의 단위로 주고 받음
	- 패킷이라는 정보의 덩어리를 만들어, 덩어리가 목적지까지 잘 갈 수 있게끔 하는 것이 네트워크의 기능 
	- 어떤 호스트에서 패킷이 출발했을 때 그 패킷을 다음 라우터로 어디로 보낼 것인지 패킷스위치가 정해서 해당 패킷이 목적지까지 잘 도달할 수 있도록 정해줌

![two](/img/Network/Introduction/two.png)


- 인터넷은 네트워크의 네트워크라고 함(ISP는 인터넷 서비스를 제공하는 업체)
- 프로토콜은 어떤 정보를 서로 주고받을 때 약속이 필요함, 그런것들을 프로토콜이라고 함 
- 프로토콜을 정의하는 곳이 있음(표준을 만듬) -> Internet standards에서 정함(계속 업데이트 됨)

![three](/img/Network/Introduction/three.png)


- Internet의 service의 관점 
- 다양한 응용프로그램을 제공하는 관점(웹, 음성통화, 이메일, 게임 등을 제공하는 인프라)
- 이를 위해서 소켓 프로그래밍이 필요함, 어떤 기기에서 다른 기기로 통신을 할 수 있게함 

![four](/img/Network/Introduction/four.png)
![five](/img/Network/Introduction/five.png)


- 프로토콜이란?
- 정보를 서로 주고 받기 위한 약속 
- 특정 메시지 정보를 보내거나 받을 때 어떤 format, 순서로 보낼지 다 정의를 하고 있음 
- 스마트폰에 정보를 보냈을 때 그 보낸 정보를 쭉 읽어서 누구한테 보내는지 주소가 적혀있음, 하고자 하는 말의 몇 번째일지, 패킷에서도 보내고자 하는 정보의 순서가 있음, 동영상 역시 마찬가지, 이러한 것을 프로토콜에서 관리를 함

## network edge
![six](/img/Network/Introduction/six.png)


- network edge
	- 네트워크의 가장 말단에서 일을 하는 것, 호스트(클라이언트와 서버)
	- 클라이언트(서비스를 요청하는 고객), 서버(데이터센터에 모여있음, 실제 사용하는 정보를 주게되는 서비스의 주체)
- physical media
	- 물리적인 통신을 가능하게 해주는 매체(구리선, 광섬유 케이블, 전파)
- access network
	- network edge에서 실제 접속을 하게 하기 위해서 기계들의 연결 & 그룹, 위의 그림에서 mobile network, home network등 그 안에 구성요소와 같이 network를 통신받고 활용되는 그러한 그룹
	- network edge들이 실제 접속을 하게 해줄 수 있는 것(core network에)
- network core
	- 인터넷의 중심을 다루고 있는 것
	- global ISP, regional ISP 등 라우터, 즉 서로간의 데이터들을 주고받을 수 있게 촘촘하게 배치되어 있음

![seven](/img/Network/Introduction/seven.png)


- Access network
- edge router
	- core에 연결이 되어 있는 router
	- 주거 단위에 있는, 회사나 학교에서 쓰는, LTE, 5G등의 네트워크
- end system
	- core에 연결되어 있는데 이 core에 연결되는 router를 통해서 전달됨
- 대역폭등 access network의 속도는 빠르지 체크해야함

![eight](/img/Network/Introduction/eight.png)


- DSL은 위와 같이 이미 존재하고 있는 전화선을 사용함, 속도는 낮은편이나 다운로드 속도가 좀 더 높음 

![nine](/img/Network/Introduction/nine.png)


- DSL이후 cable network 나옴
- FDM
	- 전선안에서 서로 다른 주파수를 갖게끔 함, 주파수를 서로 다른 것을 구분해서 한 번에 보낼 수 있음

![ten](/img/Network/Introduction/ten.png)


- 기존의 구축된 환경을 활용함 
- 최근에는 광케이블이 집근처까지 들어와서 기가급의 속도를 사용할 수 있음 

![eleven](/img/Network/Introduction/eleven.png)

- 외부와 접속이 되는 인터넷 기술이 집까지 들어왔다면 공유기를 사용해서 네트워크를 형성함, 외부 접속이 되는 modem이 있고 그 modem과 공유기를 연결시켜 IPTV, wifi 사용 가능함, 공유기(router가 그 역할을 함)

![twelve](/img/Network/Introduction/twelve.png)


- 이더넷
- 높은 전송률을 제공함(집에서도 사용 가능함)

![thirteen](/img/Network/Introduction/thirteen.png)


- 무선 네트워크는 access point, 기지국을 활용함(무선 기계들이 무선 신호를 사용해서 인터넷에 접속을 할 수 있게 해 줌)
- wifi가 주로 사용됨, LAN(Local Area Network)
- Wifi는 IEEE가 표준화시킴, 다양한 넘버링 진행(802.11), 가장 일반적으로 이야기 하는 무선랜, 빌딩안, 수십미터 정도의 거리를 커버하기 위해 나온 기술, 킬로미터 단위로 떨어지면 사용힘듬, 집안 건물에서 많이 씀 
- wide-area wireless access는 넓은 지역을 커버함, celluar(이동통신), 4G(LTE), 5G등 수킬로미터에서 수십킬로미터에서까지 인터넷, 기기와 통신을 할 수 있게끔 설계가 되어있음, 이동을 하면서 쓸 수 있게끔 사용하는 것, 넓은 영역 커버 가능

![fourteen](/img/Network/Introduction/fourteen.png)

- 호스트가 어떻게 주고 받을 것인가
- 컴퓨터에서 정보를 전송할 때 패킷이라는 단위로 활용함, 패킷은 L비트로 이루어져 있음 
- access network의 링크의 전송률은 R로 구성되어 있음, delay가 어떻게 되는지 구할 수 있음 
- 전송률은 링크를 통한 것이라 링크의 전송용량 capacity에 의해서 정해지는 것, 이것을 link bandwidth라고 함
- L bit를 R(bits/sec)이라는 전송률을 가지는 것으로 L/R을 하면 결국 sec만 남아 몇초가 걸리는지 확인함 

![fifteen](/img/Network/Introduction/fifteen.png)


- 실제 communication link를 만들 때 물리적인 매체에 의해서 만들게 됨
- communication link의 대역폭은 어떤 물리적인 매체를 사용하느냐에 따라 다름 
- 구리선부터 전자파등 다양하게 존재함 
- 통신 <-> 수신 bit를 통해서 물리적인 매체로 전달됨 
- 통신 <-> 수신 실질적으로 놓여있는 매체, physical link
- 매체가 이동하는 길이 유도가 되는지에 따라 guided, unguided로 나누어짐
- guided media
	- 케이블 랜선을 주로 말함(solid 한 매체 안에서) 신호가 매체를 통해서 유도되는 방향으로 진행이 되는 것(케이블 밖으로 신호가 나올 수 없음)
	- 케이블이 유도하는대로 신호 전송
- unguided media
	- 전송되는 신호가 자유롭게 퍼지는 것을 의미
	- 무선 전자 전파신호를 말함(공유기, 집안 어디서도 wifi를 통한 접속가능)
- twisted pair(TP)
	- 꼬임 상선, 일반적으로 사용하는 랜선케이블(다양한 선들이 존재함, 케이블을 안에서 꼬아, 신호가 전달되는데 발생하는 간섭들을 최소화함)
	- 안정적으로 신호를 보냄, Category5, Category6 등 케이블의 종류가 존재함 

![sixteen](/img/Network/Introduction/sixteen.png)


- coaxial
	- 동축 케이블, 케이블 TV를 지원하기 위해서 많이 사용됨 
- fiber optic
	- 광섬유 케이블, 인터넷 뿐 아니라 음성신호를 최대한 손실없이 사용되기도 함
	- 빛의 형태로 제공됨, 빛 그 자체가 정보를 전달하는 매체가 됨
	- 큰 대역폭 빠른 전송률 제공, 전자기파의 내성이 있음 

![seventeen](/img/Network/Introduction/seventeen.png)


- 물리적인 매체에서의 전파, 스마트폰에서 사용함 
- 정보가 전파에 실려서 전송이 됨, FM라디오 포함, 전파에는 물리적인 선이 존재하지 않음, 양방향 통신을 함 
- 환경에 의한 영향이 매우 큼
- 이제는 주로 기가급 이상의 전송률
- wifi, wide area, satellite(신호가 왔다갔다 하는 것만으로도 딜레이가 생김)

## network core
![eighteen](/img/Network/Introduction/eighteen.png)


- 수 많은 네트워크 연결(서버 - 사용자연결(network edge 연결))
- 진하게 그림 표시된 것 기준으로 출발지 - 목적지, 계속 패킷 전달(라우터 사이에서 packet switching), 진하게 표시된 부분이 network core임
- 링크를 통한 packet을 전송을 함, capacity 측정(transmission rate)

![nineteen](/img/Network/Introduction/nineteen.png)


- source에서 packet을 보내는데 L/R sec 걸림, router에서 모두 저장한 후 destination에 링크를 보냄(one-hop, 링크를 보냄)
- end-end delay, source-destination에서 router가 있으면 생기는 delay, source-destination까지 걸리는 시간
- propagation delay(거리로 인한 물리적인 딜레이, 위의 예시는 없음)
- one-hop numerical example에서 주어진 바와 같이 L,R이 주어지면 링크를 보내는데 걸리는 delay를 알 수 있음
- 추가적으로 example에서 end-end delay는 10sec가 됨

![twenty](/img/Network/Introduction/twenty.png)


- 전송률에 따라 loss가 발생하기도 함
- 위의 예시에서 router로 보내는 속도가 100Mb/s 그리고 router에서 전송을 하는데 속도가 1.5Mb/s면 router에서 보내는 속도가 더 느리므로, 병목현상이 발생함
- queue에 packet이 쌓이게 되는데 여기서 내 packet을 보내기 위해서 그 앞의 packet이 전송되어야 하는데 속도가 맞지 않아 지연시간이 생김(queueing delay)
- 도착률이 router에서 전달할 수 있는 전송용량(률)보다 커지면 router에 쌓임 -> 쌓이게 되면 앞의 패킷을 보낼때까지 기다리는 delay가 생김 -> 많이 쌓여 총 용량보다 초과되면 packet이 버려짐(packet loss)
- 용량을 생각하여 혼잡도를 관리해야함

![twentyone](/img/Network/Introduction/twentyone.png)


- routing algorithms : 출발 - 목적지가 있을 때 그 사이 어떤 경로를 따라서 packet을 전송할 지 결정하는 것
- 각각의 router에 local forwarding table이 정해져 있음(다은 router에 저장하고 그 이후 forwarding함)
- forwarding : 어떤 router에서 그 packet을 특정 packet의 다음 어느 router 어디에 보낼것인지 정하는 것

![twentytwo](/img/Network/Introduction/twentytwo.png)


- 위 통신은 전화에 많이 사용이 됨
- reserved for call(통신을 위한 자원이 아예 예약됨), no sharing, 아예 예약이 되어 있으므로, 항상 쓸 수 있는 통신 자원이 예약됨
- 즉 위의 예시에서 A->B로 갈때 예시의 루트대로만 갈 수 있고 다른 곳은 갈 수가 없음

![twentythree](/img/Network/Introduction/twentythree.png)


- 언제든 사용가능하게 나뉘어져 있음
- FDM : Frequency 기준으로 여러 유저를 서비스 해줌, frequency 축을 나눠서 쪼개서 동시에 서비스함
- TDM : Time을 잘게 쪼개서 서비스함

![twentyfour](/img/Network/Introduction/twentyfour.png)


- 1Mb/s link를 쓰고 user는 100kb/s를 쓰면서 10% 시간만을 사용함
- circuit switching의 경우 각각 나눠서 서비스를 하므로 100x10=1Mb/s이므로 10명의 유저만 사용함
- packet switching의 경우 보낼때 확 보내면서 안 보낼떄는 쉬게 되는데 여기서 동시에 10명이 보내질 확률이 극히 적으므로 더 많은 유저를 보낼 수 있음

![twentyfive](/img/Network/Introduction/twentyfive.png)


- bursty data의 경우 packet을 대부분 안보내다 보낼때 확 보내는 상황에서 packet이 유리함(sharing을 할 수 있으니깐)
- 그래도 delay와 loss의 여지가 있으므로 무조건 좋은 것은 아님(data가 확 늘어난다면) -> 이를 해결하기 위해 protocol & congestion control을 함
- circuit-like 같은 경우는 대역폭이 보장된 경우 필요로 하고 특수한 상황(자율주행차 통신 등)이런 상황에서는 circuit switching을 고려하나 아직도 미해결 과제임

![twentysix](/img/Network/Introduction/twentysix.png)


- ISP도 서로 간 연결되어야 인터넷을 할 수 있음
- 독립된 네트워크를 인트라넷이라고함(내부에서만 사용)

![twentyseven](/img/Network/Introduction/twentyseven.png)


- 모두 다 일일이 하나하나 연결할 수도 없고 상당히 복잡해짐

![twentyeight](/img/Network/Introduction/twentyeight.png)


- local한 access network를 가운데서 연결한다면 서로간 연결 할 필요없이 global ISP를 통해 link를 만들 수 있음

![twentynine](/img/Network/Introduction/twentynine.png)
![thirty](/img/Network/Introduction/thirty.png)


- 하지만 단일한 ISP만 존재하지 않고 다양한 ISP가 존재함
- 이들 역시 서로 연결시켜줘야 하므로 IXP가 생김

![thirtyone](/img/Network/Introduction/thirtyone.png)
![thirtytwo](/img/Network/Introduction/thirtytwo.png)


- 지역별로 연결해주는 ISP도 존재함(굉장히 복잡히 연결)
- content provider networks -> 본인들만의 네트워크 존재함(Google, Microsoft, Akamai...)

![thirtythree](/img/Network/Introduction/thirtythree.png)
![thirtyfour](/img/Network/Introduction/thirtyfour.png)


- 이외에도 다양하고 규모가 큰 연결망이 존재함

## delay, loss, throughput in networks
![thirtyfive](/img/Network/Introduction/thirtyfive.png)


- queue에서 packet loss가 발생함, 전송시 delay가 위와 같이 생기면서 꽉차게 되는경우 loss 발생

![thirtysix](/img/Network/Introduction/thirtysix.png)
![thirtyseven](/img/Network/Introduction/thirtyseven.png)


- d(proc)->nodal processing : router에서 packet 체크 및 보내기 위한 결정시간등으로 인한 delay
- d(queue)->queueing delay : router 도착시 packet이 많으면 delay(혼잡도 높으면 delay 높아짐)
- d(trans)->transmission delay : L/R, 패킷 전송시 소용되는 delay
- d(prop)->propagation delay : d/s, 물리적으로 신호가 도달하는데 걸리는 시간(정보가 전파되는 속도 router간 물리적거리)

![thirtyeight](/img/Network/Introduction/thirtyeight.png)
![thirtynine](/img/Network/Introduction/thirtynine.png)

- 첫번째 예시에서 toll booth를 지나가는데 즉 router를 통과해 queue를 가는데 12초가 걸림 총 10대의 차가 있으므로 120초가 걸림
- 그리고 다음 toll booth까지 100km/h를 가니깐 1hr이 걸림
- 그래서 2번째 toll booth에 line up을 하는데는 60min + 2min인 62min이 걸림 
- 두번째 예시에서는 propagate가 1000km/h임 즉 지나는시간이 6min이 걸리는것임, 그리고 toll booth에서의 시간이 1min이 걸린다고 함, 그래서 하나의 차가 7min이 지나고 도착하면 이 도착한 차는 2번째 toll booth에서 계산을 한 후 지나갈 수 있으므로 첫번째 toll booth에서 서비스 받기 전에 이미 두번째 toll booth에서 처리를 한 뒤 나갈 수 있음

![fourty](/img/Network/Introduction/fourty.png)

- Packet이 어떤식으로 도착햐냐에 따라 양상이 다름
- La(1초에 도착하는 bit수)/R(1초에 해당 router에서 밖으로 보내주는 bit수)
- 0에 가까우면 queueing delay가 작고, 1에 가까워지면 queueing delay가 커짐(1보다 크면 들어오는 bit수가 나가는 bit수보다 커짐,발산함)
- 1보다 크면 무한대가 됨(lim에서 a를 1로 보내지면 발산을 하는 것)

![fourtyone](/img/Network/Introduction/fourtyone.png)
![fourtytwo](/img/Network/Introduction/fourtytwo.png)

- 인터넷에서는 이렇나 차이를 느끼기 힘들고, 실제 인터넷에서는 traceroute를 통해서 delay를 체크함(번호가 router를 의미함)

![fourtythree](/img/Network/Introduction/fourtythree.png)

- queue에 buffer가 가득차면 packet을 버림, 그때 packet loss가 발생함

![fourtyfour](/img/Network/Introduction/fourtyfour.png)
![fourtyfive](/img/Network/Introduction/fourtyfive.png)
![fourtysix](/img/Network/Introduction/fourtysix.png)

- Throughput은 전송률을 의미함
- rate:단위시간당 몇 bit를 보냈는가(sender/receiver, 보내는쪽/받는쪽 사이의 전송률을 의미함)
- instantaneous:한순간의 throughput(단위시간당 전송 bit)
- average:특정시간동안 얼만큼의 bit을 보냈는지
- 출발/목적지 사이의 링크 고려 throughput구함
- 여기서 Rs,Rc가 서로 다를 수 있음, 그때 전송속도가 느린곳에서 병목현상 발생함
- bottleneck link : 전송속도 느린곳에 병목현상 발생(국내 vs 해외 사이트 비교)
- Internet scenario처럼 네트워크 코어를 활용할 수 있음, 그러나 링크마다 속도가 달라 병목현상이 생길수도 있고 크기가 큰 데이터 처리하다가 생길수도 있음

## protocol layers, service models
![fourtyseven](/img/Network/Introduction/fourtyseven.png)
![fourtyeight](/img/Network/Introduction/fourtyseven.png)

- 효율적 이해-구성을 위해 계층화를 시키면 좋음 pieces로 나뉘어져 있으니깐
- 2번째 예시처럼 화살표 순서대로 각각의 단계를 밟아서 무언가 복잡한 것을 수행하면 편안한게 처리가능함
- 즉 각각의 layer에서 수행하는 일이 있고 그 일을 수행하기 위해서 점점 더 아래 layer로 가서 결국 packet을 서로 간의 전달할 수 있도록 밑 단계에선 링크로 데이터가 가고 도착 데이터는 다시 계층을 거꾸로 올라가서 수신함
- 이러한 일련의 과정을 생각하며 layer를 형성하고 활용함

![fourtynine](/img/Network/Introduction/fourtynine.png)

- 위는 일반적인 layer층임
- transport는 데이터 정의 protocol이고 network를 통해 어떤 경로로 갈 지 결정을 하고 link를 통해 근처에 있는 다른기기와 어떻게 통신할 지 정하며 physical을 통해 유무선링크로 0/1로 구성된 bit가 전송됨

![fifty](/img/Network/Introduction/fifty.png)

- 7개의 layer 모델임, 일반적으로 5개의 layer를 사용함
- 위와같은 모델은 2개가 추가됐지만 해당 단계는 application level에서 충분히 고려해서 사용할 수 있음 

![fiftyone](/img/Network/Introduction/fiftyone.png)

- 위와 같은 과정을 통해서 bit가 전송되는데 각각 layer별로 Encapsulation을 하여서 데이터를 보내고 forwarding을 함, 그러면서 각각의 layer에 맞게 해당 데이터르 분석하고 보내면서 Encapsulation을 함
- 최종적으로 도착한 곳에서는 Encapsulation을 다 벗겨내면서 데이터를 받음