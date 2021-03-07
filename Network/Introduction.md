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