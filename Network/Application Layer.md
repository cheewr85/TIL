## Appplication layer

## Roadmap
- [principles of network applications](#principles-of-network-applications)
- [Web and HTTP](#Web-and-HTTP)
- [electronic mail](#electronic-mail)
- [DNS](#DNS)
- [P2P applications](#P2P-applications)
- [video streaming and content distribution](#video-straming-and-content-distribution)
- [socket programming with UDP and TCP](#socket-programming-with-UDP-and-TCP)

## principles of network applications
- application layer -> 인터넷을 통해 사용하는 서비스들(이메일, 웹서핑, 카톡, 웹엑스 미팅등)
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/bfa00442-661d-4d48-8337-cad9fcebe83f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T020919Z&X-Amz-Expires=86400&X-Amz-Signature=5da82fc89f7a77080d2fdae96cfe3a4a566d001256c43fc4c650f424e9652c08&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 모두 다 network application임

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ae6fe92c-5030-434f-ab06-d0f7f024599d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T021008Z&X-Amz-Expires=86400&X-Amz-Signature=07b1831d84ac900c984ec3bb7a29c478db92aa3c0d81665e89a7a5cf1eef01e4&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- networrk app은 network의 통신을 위한 application임
- end system에서 돌아감(network), 사용자-사용자, 서버-사용자 네트워크 통해서 통신
- 둘간의 통신, 패킷을 보내지만 network-core에서 어떻게 전달되는지 다 만들 필요없음 -> 계층화(패킷들이 어떻게 목적지로 보내야하는지 신경 쓸 필요없음) -> 알아서 보냄
- application은 end system끼리의 통신, layer를 통해 알아서 연결이 됨
- 대표적인 application 구조
	- client-server
	- peer-to-peer(P2P)
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ec416fa5-0e73-40d6-b641-963c2110d84c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T021303Z&X-Amz-Expires=86400&X-Amz-Signature=623d51096d36300702fd1949b17ed3e17994e5108fce70cc7c5e34f5ba987553&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- server
	- 항상 켜져있음
	- 변하지않는 IP 주소
	- 데이터 센터 존재함 
- clients
	- 스마트폰등
	- 서버와 통신(필요할 때만)
	- 고객이므로 IP 주소는 바뀜
	- client끼리 통신할 수 없음

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6713cc74-95b3-416f-b5d7-98ad6279a94d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T021417Z&X-Amz-Expires=86400&X-Amz-Signature=5d284846ea02d8cb6e7fa2373afbe8fedbe605b84f636bcbe28baa252ba4dac4&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- Client끼리 통신
- 필요할 때 end system에서 서로 연결, 통신
- self scalability -> 그때그때 주위기기 통신, 규모가 커져도 처리를 분산시킴(server-client는 scaling을 위해 데이터센터가 존재함, 많은 사용자 처리해야하므로)
- 안정적이지 못하고 p2p 참여기기를 관리할 수 없음
- 토렌트 -> 파일 주고받은 특정 파일 여러 사용자에게 나눠 받음, 그때그때 다름, 전송 & 사용자 다름 & 사용자끼리 통신

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7030c419-9223-424e-94cb-090e926bbb42/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T021814Z&X-Amz-Expires=86400&X-Amz-Signature=e68d72b29be9d1fc5e7c9a88a1da995b4c0266ad38207602825d7c50329a4c3e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- process는 program 관리단위임
	- network application 통신, process들간의 통신(컴퓨터상)
	- end system에서 실행되고 있는 program
		- client process(웹서핑 시작, 통신개시)
		- server process(상시대기)
- inter-process communication -> 같은 host에서 내부적으로 통신(컴퓨터내), OS(network 필요없음)
- message -> 서로 다른 host에 있는 process들끼리 통신을 함(네트워크 통해 message 주고 받음)
- P2P의 경우 어떤것이든 client & server가 될 수 있음

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4c77dfe2-b9e8-4480-91cc-d556bab6a5f9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T022205Z&X-Amz-Expires=86400&X-Amz-Signature=b559a704cbc375e665e568b36b49e605b67afc3cd436179217d52a4a27c0aafa&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- message를 보내기 위한 door 역할
- process들 간의 통신을 위한 네트워크를 위한 통신을 위해 사용되는 구조를 socket이라고함

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/151de2e2-f2fb-49e9-aa11-fed05130711b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T022350Z&X-Amz-Expires=86400&X-Amz-Signature=b75711c2472878702ce6ea8b4d0bac314951c9075c5ed059ca3725ac74370ae8&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 목적지를 어떻게 인식할지 
- host를 가지고 있음, IP주소만으로 어디로 가야할지 인식힘듬 -> port number 활용

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/022ab168-093b-446d-a7b0-346c17da8f8c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T022512Z&X-Amz-Expires=86400&X-Amz-Signature=b49d4d2b89d2f69e1e63a3eccb881deee421655b7d8d70e61ff6f11c412d0cd6&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- open protocols
	- 누구나 사용가능
- proprietary protocols
	- 앱을 통해서만 서비스 활용, 회사내에서만 제공

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0adbf868-6dac-4145-8c85-21268bf603d7/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T022619Z&X-Amz-Expires=86400&X-Amz-Signature=da4068fc0cdc437f0718c62057e8f7d2684891487a6478a96bc14aab5b639c13&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- network의 필요한 요구조건
	- data integrity(데이터 무결점성)
		- 100% reliable 수신 필요
	- timing
		- 완벽할 필요는 없지만 어느정도 timing 필요(low delay)
		- delay가 너무 길면 안됨
	- throughput(전송률)
		- 동영상 이외에는 큰 필요없지만 동영상은 전송률이 높아야함
	- security(보안)
	- application layer에서 하위 layer부터 목적지까지 데이터 전달하는데 필요한 성능(지표등)
	- network core를 통해 전송을 할 때 필요로 하는 것
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f2eb67e7-cb40-4eb3-8296-89a2ab747246/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T022905Z&X-Amz-Expires=86400&X-Amz-Signature=ad49e85f44b3551914365e6e7f84e05302246aa4452ee8b320b60c46eb6368c7&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/985884d2-1271-4f98-9c48-8f234e2cc12a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T023025Z&X-Amz-Expires=86400&X-Amz-Signature=c01a8380132f2d95840e53661ac27f6beb385ae0641110dc331189da71918790&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- application에서 아래 계층에서 지원해주기 위해 구성된 service, 요구조건에 따라서 사용

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/fa07dd85-b7d7-483e-a163-d9a4622ab580/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T023134Z&X-Amz-Expires=86400&X-Amz-Signature=ca26c11a3dd2dede2a00f5c1f25752a80f6cd9a00efd746437eb46583e5199aa&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- application layer에서 어떤 protocol을 만든 후 service를 제공할 때, socket에서 transport layer로 내가 원하는 메시지를 밀어넣어 반대쪽 socket으로 나오게 할때 transport에서 어떤 service를 이용해서(어떤 protocol) 전송을 할것이냐를 결정해야함

## Web and HTTP
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/97228ef2-0805-46e5-83ed-b6b57429ef2e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T023359Z&X-Amz-Expires=86400&X-Amz-Signature=f0c7ec53474f322d6144530f6bd5c23ab503bff2468577b2fac48afbdc9472a0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/aca05f0b-68c2-406d-8606-4052b05da580/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T023454Z&X-Amz-Expires=86400&X-Amz-Signature=5f2f7581237a36f30861f2affe66f18442adaf1af3ccb68559e215cd1f947bf2&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6a91462a-85b9-4b46-a14c-811e9907a0d4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T023514Z&X-Amz-Expires=86400&X-Amz-Signature=4409d83d0bf60b3119d3b3085469f679e186b7411025c4ca6585956d7fc7d5fe&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
- HTTP(Hyper-Text-Transfer-Protocol)

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/78b3fef0-10ef-409a-b201-5560cf5a6fd6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T023607Z&X-Amz-Expires=86400&X-Amz-Signature=daed59fbb70a6577be42a240b1b1a3f26ebafa22d9b0954150bec82dcf3531da&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- non-persistent HTTP
	- 지속되지 않고 매번 열고 닫고를 고려함
	- 여러개가 있다면 여러개 열림 
	- 한개의 object 보낼 때 매번 한개의 object마다 TCP Connection을 만들었다가 닫았다가 함(object마다 connection 다르게함)
- persistent HTTP
	- 한 번 열어놓으면 여러개 연결 & 유지가능

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7eb53c08-b60c-459a-b1a2-7a86584cc530/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T023747Z&X-Amz-Expires=86400&X-Amz-Signature=54cc4282c613d41ce7307badacc628a39c4415a40abf3a4d181f65a79295b796&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/fce59c59-76cb-47de-8fb1-0411e16f7fdc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T023822Z&X-Amz-Expires=86400&X-Amz-Signature=20b2ef35bff1a5c41b27bfbc4bd0f08aae91f334a3676d1092b91c50403794c4&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c5fee671-bcf7-4b26-8b85-bc53c12d107a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T023847Z&X-Amz-Expires=86400&X-Amz-Signature=d1051af33d1d167d733669c0b2320753a7b6bf33ae9777ae40de66e88885b3b3&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- RTT(Round-Trip-Time)
	- 한 번 갔다가 오는 시간
	- object 많으면 시간 더 걸림(non-persistent의 경우)

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5e2891c7-459a-4b4c-bbdc-1aea849aad29/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T024029Z&X-Amz-Expires=86400&X-Amz-Signature=3819c558f6e983fdcdbda553444c6b6aead19b29521d4916063fd82525618d20&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- non-persistent
	- 끊고 연결 계속 관리해야함
	- 병렬적 관리시 괜찮음
- persistent
	- connect을 열어두고 통신, response 기다리지 않고 request 여러개 보내 수신 가능
	- 하나하나 여는것보다 유용
- pipelining
	- request 여러개 보내고 각각의 response를 받음

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/79544de6-fd73-4134-93ca-447fbadf7920/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T024211Z&X-Amz-Expires=86400&X-Amz-Signature=1266fdcf34fd216eaf3fa2f32e13b443714945767ab767a5c81f14c8e80ddcbd&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- header lines의 경우 어떤식으로 HTTP가 작동할지 정보를 보여줌

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2bb38d4a-f3a3-4f14-9ba2-0a2beea672e4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T024255Z&X-Amz-Expires=86400&X-Amz-Signature=f7df93f36c062b88ec397b6b0aa608e7e146f0e500f74c2291ed1af55a954dc2&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8fbba476-1373-46c0-ad31-acd4cd55240a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T024334Z&X-Amz-Expires=86400&X-Amz-Signature=66ee1a18d435033ec0a6f5c948925b50873b0ac92822972378643021d3dcd99e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- POST
	- 정보를 보내줌, server로 보냄
- URL method
	- 업로드할 정보를 담아서 보냄

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4111cd04-b3dc-43f4-b2d9-e6df3097b720/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T024431Z&X-Amz-Expires=86400&X-Amz-Signature=41fefc26caf80ea81e3d3db69cc5437573cccbb9f03bc88a7b0b9d1a47ef069e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5baa6d03-83dd-4582-aaae-f42468c7d847/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T024456Z&X-Amz-Expires=86400&X-Amz-Signature=44ab8e88d361dc36ba49943296a848d33843b7b95c3eff628de37c6ce18e8bd0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0ac04dfa-33b5-4b8d-986b-a5a9591d97b8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T024529Z&X-Amz-Expires=86400&X-Amz-Signature=64850a8b1fd0d51ef6e5bb5d42e95135471619341a6e7ae66cefe3f2cda1ee57&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 쿠키
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a1e4525d-e677-499b-96ec-ec2307662538/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T024557Z&X-Amz-Expires=86400&X-Amz-Signature=b9f2ed98d3d1ed14379912268498ffd20ea73a9e363f99b7d01fd4e3424708e5&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 유저의 상태 저장 필요
- 쿠키 아이디 사용자 저장 추적가능(유저의 상태 포함)

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6a197bb9-fcb2-4f98-b41f-7ad76df692aa/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T024648Z&X-Amz-Expires=86400&X-Amz-Signature=6865551e1796f013ffdd23472be6d45cde46b662c0ecbec4907cc5a7bb6dbb15&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/502fa1ca-6079-4a1e-901a-8b5b11c38792/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210319%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210319T024708Z&X-Amz-Expires=86400&X-Amz-Signature=98596ce9524d739a447a736f35cd67b8d5d529c4c49b55bf27bb5eaaeceeb082&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

## electronic mail
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/683c9f52-d6ea-4c98-902e-5d6bf0e5ea54/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T052838Z&X-Amz-Expires=86400&X-Amz-Signature=591145125d17bb6e123eb5117a0be1c1d8cfa62dd4625786271369f4550350cd&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- user agent는 주로 쓰는 스마트폰 메일앱과 이메일 프로그램등을 의미함(outlook, Gmail-웹페이지에서 구성됨)
- mail server는 이메일 서로 주고받을 때 그 과정에 필요한 server임
- SMTP는 메일 서버 사이에 서로 주고받는 것임(Gmail과 Naver가 서로 메일을 주고 받을 수 있게끔)
- 메일을 보내게 되면 queue에 보낼 메일이 쌓여있음
- outgoing message queue
	- message를 담고 있는(줄 세워둠)
- user mailbox
	- 여러 유저들 존재, 각각의 유저들에게 곧 메일박스가 mail server에 존재함, 각각 다른 유저임

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8b8bbfcd-51be-4509-b168-0b21fbd834e2/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T053219Z&X-Amz-Expires=86400&X-Amz-Signature=0058bccb0069d95388cde6d217991d856902641c72a8d26f46fea739c96b906d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 언제 메일이 올 지 모르기 때문에 mail server는 따로 두고 항상 켜져있음
- client - sever 구조가 형성됨 즉, 보내는 서버-받는 서버의 구조, 주고 받는 입장에서 client-server 관계가 형성됨

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/20da138c-3116-4576-a580-3a81b3fcdb08/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T053357Z&X-Amz-Expires=86400&X-Amz-Signature=deeca25783029e913525715e233b8ef7fad96b99c2a030f0a63a6ae9a7c47539&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 가장 믿을 만한 TCP 통신을 하고 port 25를 씀
- transfer에 있어서 3가지 phase가 있음(SMTP를 보내는데)
	- handshaking(greeting), 서로 인식(Gmail, Naver인지 서로 확인)
	- transferr of message, 내용 보냄
	- closure, 종료
- HTTP와 유사함, command 보내면 서버가 responseㅎㅁ
- 7-bit ASCII로 해야하는 제약조건이 있음

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/27c847c6-7fd3-4cf1-a673-0e2e71b9f57f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T053623Z&X-Amz-Expires=86400&X-Amz-Signature=d18140cc694bbed816227a3dd6b21ed7c65863b71f687aaf54c2725ab48382ab&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- mail server에 전송되는 과정
- SMTP를 통한 server 통신
- 이를 mail box에 저장, 확인함

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/466589f0-17df-44ba-adf0-5df25bedbb82/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T053743Z&X-Amz-Expires=86400&X-Amz-Signature=69cb09c2d149346573f685e56884279b4beef2c0fdaa487b40bfb07858707d2c&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 끝날때까지 연결 지속
- 문자열을 활용(메시지 종류 표현)
- HTTP 
	- pull 방식, 서버에 저장된 데이터 가져오는 것이 목적(수신하는 입장에서 웹브라우저가 TCP Connection 초기화, 있는 걸 가져와 pull)
	- Command는 ASCII, body, 파일 보낼 땐 아님
- SMTP
	- 메일 보내는 입장, 보낼거라고 Client-Server에 요청(미리 읽음, mail 밀어넣어 push)
	- body까지도 ASCII, ASCII 인코딩 때문에 달라짐

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e5a0cbf4-7d72-4776-87ae-e63a592c3c0f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T054029Z&X-Amz-Expires=86400&X-Amz-Signature=a91e2fa91bf0c3c04c1deb2d6f4f3ee775fec0482e9f8353cf30dcd1328b8a76&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 보내지는 message에 관한 format, 안의 message를 어떻게 만들지, 원본 메일 보기를 통해 header에서 누가 어떻게 무엇을 보냈는지 알 수 있음

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/06e3f785-5fa9-47aa-a3ec-09547f728112/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T054149Z&X-Amz-Expires=86400&X-Amz-Signature=e94f02b0c194712f58ec1a2647dbb62716d82b4ece5328703ba5e1e3a79900c0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- SMTP는 항상 켜져있어 보내는데 무리가 없음
- mail access protocol 과정에서는 user agent가 원할 때 읽어야 하는 것이 다름, 여기서 어떻게 메일 박스에 접근할지 등, 이를 protocol을 활용함, 설정을 통해서 메일서버에 메일앱 이용가능(HTTP예시는 사이트에서 보는 것)

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1876f899-ba20-4f3f-b006-4ed49f3a165c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T054339Z&X-Amz-Expires=86400&X-Amz-Signature=0be4e2b77e24602492507ad577adbcd354e255c0cc5ae6f7881be208d620eed4&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- authorization phase
	- 메일서버에 id&pw를 입력후 인증단계
- transaction phase
	- mail이 뭐 있는지, client 요구사항 반영, 종료시 명령에따라 처리됨

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2c492735-4fb8-496b-bbcb-c2c2beff4146/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T054450Z&X-Amz-Expires=86400&X-Amz-Signature=84413030d5ee59087771f39d1a82458df53d84b180d31f983f6bf8f3c1bb8e0d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- download and delete
	- 지웠을 때 다른곳에서 볼 수 없음
- download and keep
	- 여러 클라이언트에서 볼 수 있음
- stateless
	- 같은 유저에 여러 Client, Session간 어떤것을 했는지 기억하지 못함(A Client에서 지워도 B에서는 모름)
- IMAP
	- POP3보다 복잡함
	- 서버에 message 저장
	- 폴더화 가능
	- 서버에서 message & 폴더관리, 여러 session이 있어도 각각 session에서 상태가 공유될 수 있음(유지가능)

## DNS
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/dc3f556e-7a3e-4e16-98d5-3ecc4c8fefe4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T054811Z&X-Amz-Expires=86400&X-Amz-Signature=4d704f2698fd499fb0fba01a982b29965cb109c0b2412a7fc89bd2c9b81abc80&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 사람은 다양하게 구분함, 이름이나 주민번호 여권등
- 인터넷에서는 IP가 그 역할을 함(구분), IP Address로 서로 구분함, 하지만 여기서 IP Address를 일일이 다 기억하기 어려움, 숫자를 다 외워서 기억해야함
- 이런 불편함을 극복하기 위해 Domain Name System을 활용함(google.com이 google에 들어가기 위한 IP Address를 대신해 domain을 씀)
- Domain Name System
	- 사람이 사용하기 편한 형태의 이름 붙여줌, IP Address를 다 외워서 연결할 수 없어서
	- 유일한 domain name을 특정 IP와 연결시켜줌
	- 분산적으로 구성(하나에 다 넣을 수 없음)
	- 계층적으로 구성 관리
	- name server -> 도메인에 대한 정보, Name의 정보를 가진 Server
	- host들이 name server와 통신해서 domain name을 어떤 IP와 연결이 되는건지 application-layer protocol에서 mapping을 시킴(google.com -> 해당 IP Address로 접근)

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0b9edf7f-8463-47df-bdb8-a163b081cc2d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T055346Z&X-Amz-Expires=86400&X-Amz-Signature=9a995d4534d12a6c832e234a2e57741896c03a1acbdf841d427bdeddef66791c&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- DNS services
	- domain(hostname)을 IP Address로 변환시켜줌
	- host aliasing, 복잡한 host 주소를 짧게 표현해서 나타내줌
	- mail server aliasing, mail server가 복잡하면 안되니깐 이를 해결해줌
	- 너무 많은 사용자가 있을 때 많은 IP Address를 순환시켜 알려줌, 접속시 접속 load 분산시킴
- 왜 중앙화가 안되는가?
	- 다 저장할 수 없음(수십, 수억)
	- 관리하기 힘듬
	- 물리적인 문제(거리)
	- 한 번 터지면 연결된 모든게 다 불능이 됨

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/87f5fa6a-a786-4b93-bc01-8586c00f48dc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T055619Z&X-Amz-Expires=86400&X-Amz-Signature=ef39d864694926bc046d94295b8f38ba4c50ee53e520cea4c0f88b0157000090&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 분산적 계층적으로 이루어짐
- root 기점으로 분산, 계층적으로 데이터베이스화해서 관리

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/15939169-3fdb-43f5-a57c-ec9973210f1e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T055716Z&X-Amz-Expires=86400&X-Amz-Signature=1393438a94a335f1960efcdf7b126ee75d67779571d93eee684893e35d097e13&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 가장 상위 계층, 최상위 Domain Server -> 다른 서버들이 모르면 질문을 함, 인증을 통해 관리

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1e47efd0-911f-4727-8613-ce062786cbb2/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T055806Z&X-Amz-Expires=86400&X-Amz-Signature=d73197f73321fb8a8c8d104accd5dc4569d42c555759a56e4d4fca5b5dd1e302&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- authoritative의 경우 기관 책임서버로 학교, 기관 내 IP주소를 domain과 연결함

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e1ee68c7-4953-478c-8b79-62db03e637ed/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T055905Z&X-Amz-Expires=86400&X-Amz-Signature=4e3685ef11d0b3b7c6549620f663a806c0e78a2bb3ac88e85fcc3b5f411b564a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 계층적 시스템 구조에는 포함되지 않음
- ISP, 인터넷 제공 ISP에서 원활한 제공을 위해 주로 domain name server, 인터넷 서비스 제공업체에서 IP Address를 좀 더 효율적 mapping을 위해서 제공해줌
- 매번 DNS query를 하는 것은 비효율적임, 최근 정보를 cache로 저장(바로 넘김)

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8b3ef739-8d03-44f5-91be-e545bc3d74e9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T060159Z&X-Amz-Expires=86400&X-Amz-Signature=3710f5b2599f2173e7b65d7b1aa7cf5091c92bc10a35545a7395e0f3520a19ed&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- host name을 IP Address로 DNS를 활용하여 바꿈 그 방법중 하나인 반복적 쿼리
- root에게 물어보고 TLD에게 물어보고 책임 DNS에게 물어보는 식으로 반복작업
- 하지만 여기서 local DNS에 Cache가 있으면 바로 알려줌 하지만 그렇지 않는 경우 위 작업 순대로 처리해야함

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ff78e1cd-bf3e-4fe4-85e1-e1e69d37ac92/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T060357Z&X-Amz-Expires=86400&X-Amz-Signature=5b23bc4b0913ea4853a4abc492462c539e556049ba29e3d72f056a9fd7c7c2f8&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 재귀적 쿼리, 위와 같은 과정으로 재귀로써 타고 들어가면서 답을 얻음
- 질문을 물어본 server에게 책임을 줌 root의 부담이 커지고 반복작업과 일처리가 늘어남

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f9b993d7-73ef-4ac8-90f6-ccdf4f17dd94/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T060506Z&X-Amz-Expires=86400&X-Amz-Signature=cb6ba3b24bf5f45e8d4102ff796e075e78fdaf95489d94b8a6cc1e4e5f24f0b4&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 매번 같은 반복작업은 비효율적이고 heavy함, 이를 해결하기 위해서 local에 caching을 함, 많은 사람이 요청하는 것은 local DNS server선에서 정리함, 계층적으로 부담이 줄어듬

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6ebc669d-9f85-4bd2-b98d-1e6438997d4f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T060638Z&X-Amz-Expires=86400&X-Amz-Signature=5ee2fdf9687d8eb1b46659d7f2b5e0509c0c8fea5ebf15e9fa4d2fdfc44b027b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- record 저장, 이용을 해서 IP 주소와 hostname을 mapping해 host name으로 접속이 가능함
- RR->분산적으로 저장
- type에 따라 의미하는 바가 다름

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/cfc83cd9-33bc-4025-880e-9e5c8198feeb/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T060744Z&X-Amz-Expires=86400&X-Amz-Signature=7ffe7b07ee6012d35ea609508fc6e3b3467c8863a92d98a851cf386a07ec4481&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 각각 query와 reply 구분, identification flags 하위의 계층에서 다양한 정보를 보낼 수 있음

## P2P applications
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/854bd299-b3fc-41e0-b95c-d12ff36f534f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T060911Z&X-Amz-Expires=86400&X-Amz-Signature=f39bb50a283e802743a4c674d67296d0b36da3c08c7c7eb6fc4b72727a47a687&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 항상 켜있는 server가 아님
- end system이 켜져있으면 서로 통신함
- 간혈적으로 연결, 상황에 따라 바뀜

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/862cc2e1-5b93-422d-bfd9-ec4028b5c49f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T061017Z&X-Amz-Expires=86400&X-Amz-Signature=d0c6515dd32bc94d8379893149172d643383f97670156356638f3b1beb660017&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c96641c7-0174-4028-9454-806bede6647c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T061026Z&X-Amz-Expires=86400&X-Amz-Signature=5470c6fd1b7c744d0994b6ee21bd9fa57766d2bfad261a82dd8b2493e2809b92&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 매우 큰 파일 F를 보낸다고 가정을 했을 때 server-client 구조에선 server의 한계, 제약이생김(시간이 걸림), 다운과 업로드 속도에 buttleneck이 생길 수 있음
- 두번째 사진의 식과 같이 Dc-s는 max의 해당하는 값보다는 적어도 클 것임 여기서 N 기준으로 linear하게 증가함

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c7eaad8c-fabb-4353-b587-d5c7dbb62b0c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T061234Z&X-Amz-Expires=86400&X-Amz-Signature=f068cf575f7c839bad7c83ab61c2e8103a9c6b5ad6e2998fe3baafbae51c39fe&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- P2P 이용시 server가 한 번만 밀어내면 됨, 그 이후로 알아서 분산적으로 하니깐(F가 어디로든 감, 여기저기 퍼짐)
- linear하게 증가하지만 똑같이 clients의 업로드 속도가 받은 만큼 올려줘야 하므로 linear하게 증가함
- Dp2p가 적어도 max값보다는 클 것임
- 근처에 똑같은 파일 공유시 P2P가 효율적 하지만 먼거리에서만 파일이 있다면 속도 문제로 Client-Server가 더 효율적일 수 있음

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4c3a380f-540c-4b84-8671-ec1b7a668677/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T061450Z&X-Amz-Expires=86400&X-Amz-Signature=ad9b8689a63ed5a7e46ee82e7c0a07356eaffb7897164a0b24a8c6a276f08ba4&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- Client-Server는 고정되어 있지만 P2P의 경우 분모의 업로드 속도 역시 linear하므로 Client-Server보단 증가율이 낮음(log 형태) 