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
