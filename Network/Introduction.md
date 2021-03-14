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
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6f8a72f7-d427-4091-a200-aa185e5d5a54/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T055802Z&X-Amz-Expires=86400&X-Amz-Signature=2cd28eb3976494257fa21373a682f165a339125bd18ea80a10d6d810e099b31b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

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

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/dd3430c4-3816-4117-adab-8206ca4cb706/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T060256Z&X-Amz-Expires=86400&X-Amz-Signature=b7d52dc7d0cd445040a951b53663a2a54278608d3c90edf70f97bb917867c461&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 인터넷은 네트워크의 네트워크라고 함(ISP는 인터넷 서비스를 제공하는 업체)
- 프로토콜은 어떤 정보를 서로 주고받을 때 약속이 필요함, 그런것들을 프로토콜이라고 함 
- 프로토콜을 정의하는 곳이 있음(표준을 만듬) -> Internet standards에서 정함(계속 업데이트 됨)

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7531edce-70c8-461a-bb3b-6756f9d9e141/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T060410Z&X-Amz-Expires=86400&X-Amz-Signature=0817fdb5c673d037489eef97122e0ee8ed04311e59952a0d8f6952cd62fe43ef&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- Internet의 service의 관점 
- 다양한 응용프로그램을 제공하는 관점(웹, 음성통화, 이메일, 게임 등을 제공하는 인프라)
- 이를 위해서 소켓 프로그래밍이 필요함, 어떤 기기에서 다른 기기로 통신을 할 수 있게함 

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f3e11140-8448-42f2-bd0a-e504e0a4fabc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T060502Z&X-Amz-Expires=86400&X-Amz-Signature=f06c05d5db1f69f1199b80796a678a944e4cad262c8a3a68d6ad4496e3b1eeb8&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/62bd509f-05c2-45e3-9834-365712f61bba/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T060548Z&X-Amz-Expires=86400&X-Amz-Signature=7f5e06fb12e7739632548b69d70999c37bc4586bcfbfc8bf3994a577f2e39cb7&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 프로토콜이란?
- 정보를 서로 주고 받기 위한 약속 
- 특정 메시지 정보를 보내거나 받을 때 어떤 format, 순서로 보낼지 다 정의를 하고 있음 
- 스마트폰에 정보를 보냈을 때 그 보낸 정보를 쭉 읽어서 누구한테 보내는지 주소가 적혀있음, 하고자 하는 말의 몇 번째일지, 패킷에서도 보내고자 하는 정보의 순서가 있음, 동영상 역시 마찬가지, 이러한 것을 프로토콜에서 관리를 함

## network edge
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8839010c-a750-4c7c-90b2-030336473b51/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T060715Z&X-Amz-Expires=86400&X-Amz-Signature=8c6e2f78fa8b23c9cff0294027e17d01e2c5fe14ce78aace840df2073d654b4e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

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

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5674df06-660d-45ae-a045-e96c9edcc946/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T061023Z&X-Amz-Expires=86400&X-Amz-Signature=728c234c523c6fa95293807859fd700cfd3b1b08c999257c9d09f865bd578c1d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- Access network
- edge router
	- core에 연결이 되어 있는 router
	- 주거 단위에 있는, 회사나 학교에서 쓰는, LTE, 5G등의 네트워크
- end system
	- core에 연결되어 있는데 이 core에 연결되는 router를 통해서 전달됨
- 대역폭등 access network의 속도는 빠르지 체크해야함

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ff328a57-3eec-4dbd-baad-d991efea5e33/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T061216Z&X-Amz-Expires=86400&X-Amz-Signature=6f12c3ef843860391ab7b06e763674c80c585cbbc3a07298a6faee7d91cc6b3b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- DSL은 위와 같이 이미 존재하고 있는 전화선을 사용함, 속도는 낮은편이나 다운로드 속도가 좀 더 높음 

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ee13812d-ea8b-4b37-8cfd-ccb8497686e8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T061258Z&X-Amz-Expires=86400&X-Amz-Signature=27f2f7c854d7b00995249aabdbe0ac7cd1b4b6430d485b89a96754f991207e4b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- DSL이후 cable network 나옴
- FDM
	- 전선안에서 서로 다른 주파수를 갖게끔 함, 주파수를 서로 다른 것을 구분해서 한 번에 보낼 수 있음

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/34227eca-afbf-475f-87a9-ba43d91781d4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T061347Z&X-Amz-Expires=86400&X-Amz-Signature=9919675f22dd182717b3550210f6d584c31ccc99e1ea1bbc1660160cc190ef63&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 기존의 구축된 환경을 활용함 
- 최근에는 광케이블이 집근처까지 들어와서 기가급의 속도를 사용할 수 있음 

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/aff7da68-86f3-4600-b86b-b5497aedf84a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T061417Z&X-Amz-Expires=86400&X-Amz-Signature=82e4a493311e7f70b2c00ae79d5ff1e6ad3e358931bd5c5faad267868e26a390&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 외부와 접속이 되는 인터넷 기술이 집까지 들어왔다면 공유기를 사용해서 네트워크를 형성함, 외부 접속이 되는 modem이 있고 그 modem과 공유기를 연결시켜 IPTV, wifi 사용 가능함, 공유기(router가 그 역할을 함)

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0fcd8dd8-699e-483a-871b-a3eb58d01a88/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T061528Z&X-Amz-Expires=86400&X-Amz-Signature=1909d84291cc104e31b32d63dedf65fd0d65d2e5f519e2e130e1289e7eca8c5f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 이더넷
- 높은 전송률을 제공함(집에서도 사용 가능함)

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b0fb0541-2115-478a-901c-6f3e5ee894cc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T061612Z&X-Amz-Expires=86400&X-Amz-Signature=b6f2e87c82739572bf32c0e80674b8c6f6db2c2bc0de9aeb3204c7efcc0ce75d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 무선 네트워크는 access point, 기지국을 활용함(무선 기계들이 무선 신호를 사용해서 인터넷에 접속을 할 수 있게 해 줌)
- wifi가 주로 사용됨, LAN(Local Area Network)
- Wifi는 IEEE가 표준화시킴, 다양한 넘버링 진행(802.11), 가장 일반적으로 이야기 하는 무선랜, 빌딩안, 수십미터 정도의 거리를 커버하기 위해 나온 기술, 킬로미터 단위로 떨어지면 사용힘듬, 집안 건물에서 많이 씀 
- wide-area wireless access는 넓은 지역을 커버함, celluar(이동통신), 4G(LTE), 5G등 수킬로미터에서 수십킬로미터에서까지 인터넷, 기기와 통신을 할 수 있게끔 설계가 되어있음, 이동을 하면서 쓸 수 있게끔 사용하는 것, 넓은 영역 커버 가능

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/30c30fca-5591-4a41-9f78-12e06490f792/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T061911Z&X-Amz-Expires=86400&X-Amz-Signature=3cd7e4a022b31cef7b5b4357adb1bb20d8ccbb61c904eebeb96a5d322fae33be&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 호스트가 어떻게 주고 받을 것인가
- 컴퓨터에서 정보를 전송할 때 패킷이라는 단위로 활용함, 패킷은 L비트로 이루어져 있음 
- access network의 링크의 전송률은 R로 구성되어 있음, delay가 어떻게 되는지 구할 수 있음 
- 전송률은 링크를 통한 것이라 링크의 전송용량 capacity에 의해서 정해지는 것, 이것을 link bandwidth라고 함
- L bit를 R(bits/sec)이라는 전송률을 가지는 것으로 L/R을 하면 결국 sec만 남아 몇초가 걸리는지 확인함 

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f55a8008-5dd9-4b27-a6c8-eed3e1ee6156/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T062113Z&X-Amz-Expires=86400&X-Amz-Signature=0112d9400b64c2da3c667f9f78ebf19be17a8a0effc5e705d8249e3da3118067&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

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

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/fbdc207f-7c15-405e-9483-f246515cbe2e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T062520Z&X-Amz-Expires=86400&X-Amz-Signature=641053476f79b943907cb221a9a64c9df154429b5faef81590b3e8cf9d848fa6&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- coaxial
	- 동축 케이블, 케이블 TV를 지원하기 위해서 많이 사용됨 
- fiber optic
	- 광섬유 케이블, 인터넷 뿐 아니라 음성신호를 최대한 손실없이 사용되기도 함
	- 빛의 형태로 제공됨, 빛 그 자체가 정보를 전달하는 매체가 됨
	- 큰 대역폭 빠른 전송률 제공, 전자기파의 내성이 있음 

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6538cf3a-d890-4248-b3ee-13a1a87e3e5a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210307%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210307T062633Z&X-Amz-Expires=86400&X-Amz-Signature=f68f548d446573dc024250921e359b7eb44dc5ff6f215073d07661d34a80cad3&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 물리적인 매체에서의 전파, 스마트폰에서 사용함 
- 정보가 전파에 실려서 전송이 됨, FM라디오 포함, 전파에는 물리적인 선이 존재하지 않음, 양방향 통신을 함 
- 환경에 의한 영향이 매우 큼
- 이제는 주로 기가급 이상의 전송률
- wifi, wide area, satellite(신호가 왔다갔다 하는 것만으로도 딜레이가 생김)

## network core
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f5fe0f3b-4c84-4970-9ffd-ee1552711509/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T022125Z&X-Amz-Expires=86400&X-Amz-Signature=03f73361a7517823986b118a155a3884d16a066e1d689f37e50f9c5bfe2d5ad3&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 수 많은 네트워크 연결(서버 - 사용자연결(network edge 연결))
- 진하게 그림 표시된 것 기준으로 출발지 - 목적지, 계속 패킷 전달(라우터 사이에서 packet switching), 진하게 표시된 부분이 network core임
- 링크를 통한 packet을 전송을 함, capacity 측정(transmission rate)

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/edd12cfd-4247-4105-8684-4c14564e9df8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T022401Z&X-Amz-Expires=86400&X-Amz-Signature=12eae3d6aa2d6e2e9ad79a5725a8c7d2af76d741e27a3ba60426a72f4b5196f9&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- source에서 packet을 보내는데 L/R sec 걸림, router에서 모두 저장한 후 destination에 링크를 보냄(one-hop, 링크를 보냄)
- end-end delay, source-destination에서 router가 있으면 생기는 delay, source-destination까지 걸리는 시간
- propagation delay(거리로 인한 물리적인 딜레이, 위의 예시는 없음)
- one-hop numerical example에서 주어진 바와 같이 L,R이 주어지면 링크를 보내는데 걸리는 delay를 알 수 있음
- 추가적으로 example에서 end-end delay는 10sec가 됨

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/bea1d4fa-f6d1-4af7-8cc6-50f606d8b3e5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T022913Z&X-Amz-Expires=86400&X-Amz-Signature=06c56659346b2c30b4c8528dff9147ae0472b8662704ac35e3fc25d5fb6e9436&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 전송률에 따라 loss가 발생하기도 함
- 위의 예시에서 router로 보내는 속도가 100Mb/s 그리고 router에서 전송을 하는데 속도가 1.5Mb/s면 router에서 보내는 속도가 더 느리므로, 병목현상이 발생함
- queue에 packet이 쌓이게 되는데 여기서 내 packet을 보내기 위해서 그 앞의 packet이 전송되어야 하는데 속도가 맞지 않아 지연시간이 생김(queueing delay)
- 도착률이 router에서 전달할 수 있는 전송용량(률)보다 커지면 router에 쌓임 -> 쌓이게 되면 앞의 패킷을 보낼때까지 기다리는 delay가 생김 -> 많이 쌓여 총 용량보다 초과되면 packet이 버려짐(packet loss)
- 용량을 생각하여 혼잡도를 관리해야함

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/745f531f-2fec-4713-8207-1d9a8d1e61ff/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T023634Z&X-Amz-Expires=86400&X-Amz-Signature=12fd6dfb2fafa3b8b6f94199a2f749b174d0d83852278bd845db4f4691bde9d4&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- routing algorithms : 출발 - 목적지가 있을 때 그 사이 어떤 경로를 따라서 packet을 전송할 지 결정하는 것
- 각각의 router에 local forwarding table이 정해져 있음(다은 router에 저장하고 그 이후 forwarding함)
- forwarding : 어떤 router에서 그 packet을 특정 packet의 다음 어느 router 어디에 보낼것인지 정하는 것

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/221368ac-fd8e-4548-b806-8bf42a3d4459/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T024036Z&X-Amz-Expires=86400&X-Amz-Signature=427d9cb6c2d80a3e17a7905898aa209b3709e292d8c243c0a742051b5e72d183&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 위 통신은 전화에 많이 사용이 됨
- reserved for call(통신을 위한 자원이 아예 예약됨), no sharing, 아예 예약이 되어 있으므로, 항상 쓸 수 있는 통신 자원이 예약됨
- 즉 위의 예시에서 A->B로 갈때 예시의 루트대로만 갈 수 있고 다른 곳은 갈 수가 없음

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4ce8dc96-6f54-45f1-9056-4a03d3c45fef/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T024309Z&X-Amz-Expires=86400&X-Amz-Signature=62ca7331e6032bed8939e188c1b661e1aee3278f667c046b05ee391dae82a679&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 언제든 사용가능하게 나뉘어져 있음
- FDM : Frequency 기준으로 여러 유저를 서비스 해줌, frequency 축을 나눠서 쪼개서 동시에 서비스함
- TDM : Time을 잘게 쪼개서 서비스함

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/bbf5a6cd-c1c0-44d4-b96c-80d5a07f030a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T024448Z&X-Amz-Expires=86400&X-Amz-Signature=9e2b0059358e34b39644e5ed14aedce909dfd626bbbee5ebd5bcc3bba6406ad3&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 1Mb/s link를 쓰고 user는 100kb/s를 쓰면서 10% 시간만을 사용함
- circuit switching의 경우 각각 나눠서 서비스를 하므로 100x10=1Mb/s이므로 10명의 유저만 사용함
- packet switching의 경우 보낼때 확 보내면서 안 보낼떄는 쉬게 되는데 여기서 동시에 10명이 보내질 확률이 극히 적으므로 더 많은 유저를 보낼 수 있음

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8e75d572-a334-4d55-bfe2-85ecb3c349b4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T025223Z&X-Amz-Expires=86400&X-Amz-Signature=53dd50de163fba58bad5ea70f14246570132569094d046200f61da7e121c4631&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- bursty data의 경우 packet을 대부분 안보내다 보낼때 확 보내는 상황에서 packet이 유리함(sharing을 할 수 있으니깐)
- 그래도 delay와 loss의 여지가 있으므로 무조건 좋은 것은 아님(data가 확 늘어난다면) -> 이를 해결하기 위해 protocol & congestion control을 함
- circuit-like 같은 경우는 대역폭이 보장된 경우 필요로 하고 특수한 상황(자율주행차 통신 등)이런 상황에서는 circuit switching을 고려하나 아직도 미해결 과제임

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8586a19d-d632-4e5d-bbe1-a76fb4c91861/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T030621Z&X-Amz-Expires=86400&X-Amz-Signature=01be101ec32f72fddd327880bd152032aaa0f266301872948bc71d4046751026&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- ISP도 서로 간 연결되어야 인터넷을 할 수 있음
- 독립된 네트워크를 인트라넷이라고함(내부에서만 사용)

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/25e6b050-371a-466b-b3d0-afdc1364d3c5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T030727Z&X-Amz-Expires=86400&X-Amz-Signature=1b09a5f32d5d21c771341d5a7854785901634b86560792616d1979bd971fa833&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 모두 다 일일이 하나하나 연결할 수도 없고 상당히 복잡해짐

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/40c55c6e-a4fb-420c-b8c2-db971055ea59/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T030815Z&X-Amz-Expires=86400&X-Amz-Signature=55c1750be938eacd484aceb5baef0df0199fe69e5c8142c7815dbc0647d2a4d5&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- local한 access network를 가운데서 연결한다면 서로간 연결 할 필요없이 global ISP를 통해 link를 만들 수 있음

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/467224bf-d1a7-4bd2-98b9-e2f4de18315c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T030909Z&X-Amz-Expires=86400&X-Amz-Signature=83fcc1b2a87415f6383a1f87ab4ec0d5944fb1dff4110e953906397f579c890f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/144ffb9b-546f-4062-8e63-cfb2d9bc62e0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T030947Z&X-Amz-Expires=86400&X-Amz-Signature=37ce4b6f48c925002366711b9b10d8ea38b8988686365fd8373218138189eb32&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 하지만 단일한 ISP만 존재하지 않고 다양한 ISP가 존재함
- 이들 역시 서로 연결시켜줘야 하므로 IXP가 생김

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/93a92228-9b4e-478c-afa9-b378c9c20708/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T031049Z&X-Amz-Expires=86400&X-Amz-Signature=e6b96d72eaa09370ce784614049c9b65e668d8dc4fd9b96577f00644027e1b76&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d292101d-956a-49a4-ac9b-7cdf8e6ae288/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T031059Z&X-Amz-Expires=86400&X-Amz-Signature=14565fe64d9bc8f4b5b278486aa343fcc8374a102a84dcade2f5baedcfb552e9&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 지역별로 연결해주는 ISP도 존재함(굉장히 복잡히 연결)
- content provider networks -> 본인들만의 네트워크 존재함(Google, Microsoft, Akamai...)

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7f3b009c-cdaa-4a6c-9770-53ba77593835/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T031227Z&X-Amz-Expires=86400&X-Amz-Signature=f839cb48268dbb7c63071f64290a7069d488599ec1dec92c95b3b36c4b7925dc&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/86152cea-9f29-4ae8-b057-3b525062f219/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T031235Z&X-Amz-Expires=86400&X-Amz-Signature=1414b61ea253c765765c4872c9ea9f25f9699b0fb32cf3543dcec5957a38910b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 이외에도 다양하고 규모가 큰 연결망이 존재함

## delay, loss, throughput in networks
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/72e30444-4c9d-42b9-bb0f-55cfbb583b93/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T031415Z&X-Amz-Expires=86400&X-Amz-Signature=0de32b69077e6c7b590b2d81f8d00807429a8a40cdab38ca8103d8c1324c1d45&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- queue에서 packet loss가 발생함, 전송시 delay가 위와 같이 생기면서 꽉차게 되는경우 loss 발생

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0a62a8d3-27d5-401b-aa89-257835ab884c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T031529Z&X-Amz-Expires=86400&X-Amz-Signature=01ec86d2893428df3fe12c9b7b69ad6256dd27125b0ea32f23b8b21975c7626c&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a0e99796-3a3c-4bbb-8395-cb2832ea996e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T031538Z&X-Amz-Expires=86400&X-Amz-Signature=b490bd28064a61f415c8236338ffb0c908acd88f73e0d9b3f870f5d9e2278f09&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- d(proc)->nodal processing : router에서 packet 체크 및 보내기 위한 결정시간등으로 인한 delay
- d(queue)->queueing delay : router 도착시 packet이 많으면 delay(혼잡도 높으면 delay 높아짐)
- d(trans)->transmission delay : L/R, 패킷 전송시 소용되는 delay
- d(prop)->propagation delay : d/s, 물리적으로 신호가 도달하는데 걸리는 시간(정보가 전파되는 속도 router간 물리적거리)

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d300bd31-23d9-45b6-9f72-2c597a8f3a06/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T031903Z&X-Amz-Expires=86400&X-Amz-Signature=3feb6d5bf4b0d534bead41ac8d2b29a329492a5574ec02df70e434cb4f66e6b8&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4f409f76-0092-47f5-8345-625e032e3aeb/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T031913Z&X-Amz-Expires=86400&X-Amz-Signature=4f0b8d3693a99e0aac9435f005fe356694e5a0e78041441c8e97fb55ebeed854&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 첫번째 예시에서 toll booth를 지나가는데 즉 router를 통과해 queue를 가는데 12초가 걸림 총 10대의 차가 있으므로 120초가 걸림
- 그리고 다음 toll booth까지 100km/h를 가니깐 1hr이 걸림
- 그래서 2번째 toll booth에 line up을 하는데는 60min + 2min인 62min이 걸림 
- 두번째 예시에서는 propagate가 1000km/h임 즉 지나는시간이 6min이 걸리는것임, 그리고 toll booth에서의 시간이 1min이 걸린다고 함, 그래서 하나의 차가 7min이 지나고 도착하면 이 도착한 차는 2번째 toll booth에서 계산을 한 후 지나갈 수 있으므로 첫번째 toll booth에서 서비스 받기 전에 이미 두번째 toll booth에서 처리를 한 뒤 나갈 수 있음

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/78ede89e-c887-4f61-8d27-ca7bf5f86bee/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T033731Z&X-Amz-Expires=86400&X-Amz-Signature=52267d13ac3abc50a58ccc437cc50a216160e668c38b4d0e9b7439fe561e7fcf&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- Packet이 어떤식으로 도착햐냐에 따라 양상이 다름
- La(1초에 도착하는 bit수)/R(1초에 해당 router에서 밖으로 보내주는 bit수)
- 0에 가까우면 queueing delay가 작고, 1에 가까워지면 queueing delay가 커짐(1보다 크면 들어오는 bit수가 나가는 bit수보다 커짐,발산함)
- 1보다 크면 무한대가 됨(lim에서 a를 1로 보내지면 발산을 하는 것)

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/52bf425a-8b16-42fe-ba65-956ad760b717/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T034045Z&X-Amz-Expires=86400&X-Amz-Signature=aaee7d5f6dea645f5597e1d8fec3db57b96ba80986a8a1c5bb211eafaee4da83&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7ece6f54-a582-476f-92fe-f4cc3e9ecf1c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T034054Z&X-Amz-Expires=86400&X-Amz-Signature=668866ceeb0e0a59a2da04e74edfd03b0d893c013d57101d0af903760efe9f3f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 인터넷에서는 이렇나 차이를 느끼기 힘들고, 실제 인터넷에서는 traceroute를 통해서 delay를 체크함(번호가 router를 의미함)

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8291a3ce-7a26-45ca-9f52-5ab57e7206c8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T034203Z&X-Amz-Expires=86400&X-Amz-Signature=5c62de2728140baee57ae0fc12ead97a024c58773973c85b5383ddfaeb9efa65&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- queue에 buffer가 가득차면 packet을 버림, 그때 packet loss가 발생함

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9b67c2fa-f008-49ca-8668-c4a20e5bbe63/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T034304Z&X-Amz-Expires=86400&X-Amz-Signature=1edd9463dd447d6da50ddc496aca4cf410f301c80226c6b6a35c4bfdfcbff75b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2d862c2b-0b12-452a-a330-0e2f821d1d33/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T034315Z&X-Amz-Expires=86400&X-Amz-Signature=87589da65e1bb517dfec8a04a30576dbf2c13e1de557dc085628126c781e1c2b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f9a5e005-5d6e-44b5-8258-20439a970301/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T034325Z&X-Amz-Expires=86400&X-Amz-Signature=92e8a2c00b0c6dab0b352d009618535b44cfa6cb564e495f65c04e9d47ff87ed&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- Throughput은 전송률을 의미함
- rate:단위시간당 몇 bit를 보냈는가(sender/receiver, 보내는쪽/받는쪽 사이의 전송률을 의미함)
- instantaneous:한순간의 throughput(단위시간당 전송 bit)
- average:특정시간동안 얼만큼의 bit을 보냈는지
- 출발/목적지 사이의 링크 고려 throughput구함
- 여기서 Rs,Rc가 서로 다를 수 있음, 그때 전송속도가 느린곳에서 병목현상 발생함
- bottleneck link : 전송속도 느린곳에 병목현상 발생(국내 vs 해외 사이트 비교)
- Internet scenario처럼 네트워크 코어를 활용할 수 있음, 그러나 링크마다 속도가 달라 병목현상이 생길수도 있고 크기가 큰 데이터 처리하다가 생길수도 있음

## protocol layers, service models
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/32552b7f-7cbe-473b-a49c-bf2c5d0e60b1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T034802Z&X-Amz-Expires=86400&X-Amz-Signature=7253a7c26a9322c1883f0d449cfe19d77c95c1cca1c29ff36c3389b0d4081c27&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c44778d1-619b-41a2-bdac-dfcc09851dd6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T034811Z&X-Amz-Expires=86400&X-Amz-Signature=e73706018b773d45d6ddbafd41581251177e998ca43d07922f4b315c86281538&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 효율적 이해-구성을 위해 계층화를 시키면 좋음 pieces로 나뉘어져 있으니깐
- 2번째 예시처럼 화살표 순서대로 각각의 단계를 밟아서 무언가 복잡한 것을 수행하면 편안한게 처리가능함
- 즉 각각의 layer에서 수행하는 일이 있고 그 일을 수행하기 위해서 점점 더 아래 layer로 가서 결국 packet을 서로 간의 전달할 수 있도록 밑 단계에선 링크로 데이터가 가고 도착 데이터는 다시 계층을 거꾸로 올라가서 수신함
- 이러한 일련의 과정을 생각하며 layer를 형성하고 활용함

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7d2d0b26-5302-4c54-b28b-e2276a68e0de/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T035031Z&X-Amz-Expires=86400&X-Amz-Signature=a56d241fc71d6f7ec8a9a5d7f01f816c8c95f47b7d3768fd77bf3fd148413041&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 위는 일반적인 layer층임
- transport는 데이터 정의 protocol이고 network를 통해 어떤 경로로 갈 지 결정을 하고 link를 통해 근처에 있는 다른기기와 어떻게 통신할 지 정하며 physical을 통해 유무선링크로 0/1로 구성된 bit가 전송됨

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/cdffbfd6-8eb0-4370-8040-bac7c9430437/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T035159Z&X-Amz-Expires=86400&X-Amz-Signature=f9a7816ce95997829a00aeb476e6cc863ef5d95ca5ac8eb8f5bdd2eb6be28576&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 7개의 layer 모델임, 일반적으로 5개의 layer를 사용함
- 위와같은 모델은 2개가 추가됐지만 해당 단계는 application level에서 충분히 고려해서 사용할 수 있음 

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6a4c6151-ebf6-448e-9f62-34b09d189880/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210314%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210314T035303Z&X-Amz-Expires=86400&X-Amz-Signature=ab0c6dcd7790a91c522f4e2f855b025da8d2ae5f352640646422d2f5aa5569e6&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 위와 같은 과정을 통해서 bit가 전송되는데 각각 layer별로 Encapsulation을 하여서 데이터를 보내고 forwarding을 함, 그러면서 각각의 layer에 맞게 해당 데이터르 분석하고 보내면서 Encapsulation을 함
- 최종적으로 도착한 곳에서는 Encapsulation을 다 벗겨내면서 데이터를 받음