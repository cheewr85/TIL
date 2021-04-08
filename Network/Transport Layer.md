## Transport Layer

## Roadmap
- [transport-layer services](#transport-layer-services)
- [multiplexing and demultiplexing](#multiplexing-and-demultiplexing)
- [connectionless transport UDP](#connectionless-transport-UDP)
- [principles of reliable data transfer](#principles-of-reliable-data-transfer)
- [connection-oriented transport TCP](#connection-oriented-transport-TCP)
- [principles of congestion control](#principles-of-congestion-control)
- [TCP congestion control](#TCP-congestion-control)

## transport layer services
- transport services
	- logical communication, 서로 다른 application host에서 물리적 요소를 고려하지 않는 즉 보내면 받을 수 있다는 단순 논리
- end systems(transport protocols)
	- send side : segments(network layer에 보냄, router끼리 data 주고 받음)
	- rcv(receiver) side : segments를 받아 잘 조립, 복구시켜 application으로 올림
- TCP, UDP 통신(인터넷 사용)
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b1c208a3-3387-4fb6-bae4-f0170e72be4d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T133432Z&X-Amz-Expires=86400&X-Amz-Signature=df68d401108694fa736f548ea223aacd19edaf94b51d6fc27e869a3187019b38&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- network layer
	- hosts만 논리적 연결
- transport layer
	- process간 논리적 연결
	- 끝과 끝을 연결한 터널같이 보내면 받는 물리적인 요소 고려하지 않음

- TCP(Transmission Control Protocol)
	- reliable, in-order delivery
	- congestion control
	- flow control
	- connection setup
- UDP
	- unordered delivery
	- no-frills extension of best-effort IP(최선을 다하는 디테일한 부분은 고려못할 수도 있음)
- services not available
	- delay guarantees
	- bandwidth guarantees
	- 즉 딜레이가 대역폭이 꼭 보장되는 상황에서는 쓰기 힘들 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f8a47d7b-112e-4cb7-b836-40969b44f58f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T133751Z&X-Amz-Expires=86400&X-Amz-Signature=4da42be880bda1c2922d331e6830b310bac542813b97161b93a0a9b3e922db8b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

## multiplexing and demultiplexing
- multiplexing at sender
	- 여러 process별로 socket 통신이 다름
	- 여러개 socket, 어떻게 잘 취합해서 보내는지
	- socket들 간 혼선이 있으면 안됨(header를 붙임)
- demultiplexing at receiver
	- 수신입장
	- 어떤(어느)socket으로 전달해야하는지
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8daf02ec-bd27-4fce-9a98-29b8d9c1d1bf/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T134306Z&X-Amz-Expires=86400&X-Amz-Signature=395c8d5914fcc87ecf7d1a78ee4babcac73bbfec603468b6953673462adfb784&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- Connectionless demultiplexing
	- UDP에서 사용
	- 단순하게 port nunmber를 통해서 socket 통신을 하고 port number만을 보고 해당 socket에 전달함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0fda477b-7b69-48a3-9458-39de741f6dbf/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T134455Z&X-Amz-Expires=86400&X-Amz-Signature=b95b9e627b042d561e32a09a7d075b247d1c8b165216b53472dd729a8f10fd60&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- Connection-oriented demux
	- TCP에서 사용
	- TCP socket은 4개의 식별자를 사용하여 port가 같아도 다르게 보냄, 해당 process와 연결됨
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/09a2b961-ee5f-4015-ad0f-b00959f5309a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T134609Z&X-Amz-Expires=86400&X-Amz-Signature=cf91ef9daabbf64815a9a9adf78ce7b1ca1147c067cb5116d78c79004a730660&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- port가 같아도 IP가 서로 다르고 그 안에도 port 번호가 달라서 수신이 다름
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/717b0ae2-c932-46c1-b6ee-7c07d7f894a1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T134654Z&X-Amz-Expires=86400&X-Amz-Signature=17a605414b0c7f2370479be2afef5857fc2032aec10fde77b6b7f1426f59c806&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 하지만 효율성을 위해 아래와 같이 프로세스 하나 안에서 여러 소켓을 관리함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/565ee76b-28e3-4460-8ed2-3d50c297c1a1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T134740Z&X-Amz-Expires=86400&X-Amz-Signature=d040859dd0570b504bbd56cf925d53ff0fbb5baf3fd109fe075ecec6277d30a8&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

## connectionless transport UDP
- UDP(User Datagram Protocol)[RFC 768]
	- best effort service
		- 즉 data를 잃을 수도 있고 순서대로 app에 전달을 하지 않을수도 있음
	- port number만 보고 연결함, 즉 둘간의 연결을 만들고 port number만 보고 처리하므로 독립적으로 적용
	- streaming multimedia, 즉 약간의 loss가 허용되는 곳에서 빨리 전달되면 활용함
	- application layer에 어느정도의 의존성 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ea3522e0-5864-4207-885c-b0405537dd7e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T135031Z&X-Amz-Expires=86400&X-Amz-Signature=f57dd0166439b9b29e96f8501af1a1bbdaa3ce782fc831b70229fe869979c3ac&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- checksum
	- sender에서 16-bits integers를 모두 더함
	- receiver에서 checksum을 비교해서 체크함
- wraparound 부분 기준으로 위의 두 비트를 단순하게 더함 2진수 덧셈으로 wraparound는 더해서 남는 수 이 부분을 마지막에 +1을 하여 sum으로 나타냄
- 여기서 sum과 더했을 때 모두 1이 되도록 하는 checksum을 만듬
- 이를 통해 에러 체크를 함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6d610aa0-754c-4264-8f3d-900a31ad7a47/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T135133Z&X-Amz-Expires=86400&X-Amz-Signature=758a958ad9397f010e96c670ea1f491adf5133e9341c790fcc52e99329963fda&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

## principles of reliable data transfer
- data를 신뢰성 있게 보내기 위해서 아래와 같은 과정이 필요함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c1c572f6-1f69-4c9a-914e-6f75750ca5e9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T215510Z&X-Amz-Expires=86400&X-Amz-Signature=8e0dc10a41b5f671e380e459236e3b18742ea27dbaf4a778671a8ed1bb85ba56&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- (b)부분에서 unreliable channel을 이용하기 때문에 다양한 loss가 일어나고 reliable하지 못함
- 그렇기 때문에 reliable하게 data를 보낼 수 있는 protocol이 필요한 것이고 (b)와 같은 일련의 과정이 필요함, 데이터를 보내고 복원하는 과정이 필요

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/174d7570-377b-4f7c-87bf-0a3ce6c0744c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T215739Z&X-Amz-Expires=86400&X-Amz-Signature=c7df0680b78e54140c4f222064bdc8f7272a493d45eb575fe6b34e911a4f5aa0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- reliable data transfer를 위해서 위와 같은 일반적인 형태의 protocol이 있음
- rdt_send()를 통해서 reliable하게 data를 보내게끔 처리한 후
- udt_send()를 통해서 protocol에서 아래의 layer로 보게함(unreliable channel)
- 그리고 unreliable channel을 통해서 data가 전달되고 여기서 unreliable channel은 물리적인 communication channel임
- rdt_rcv()를 통해 packet이 도착했다고 보내주는 호출을 하고
- deliver_data()를 통해 수신된 packet을 활용, 상위 layer로 보내느 과정을 거침
- 위와 같은 방식으로 해야 Reliable data transfer가 가능함

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b409f3e4-2c2e-4f8a-bc9c-778160328e5a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T220117Z&X-Amz-Expires=86400&X-Amz-Signature=268bdfdba17516adc596d7db53fa7430d5e9b95388e584196868d89b90322983&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 이를 위해 reliable data transfer(rdt) protocol의 사용과 finite state machines(FSM)을 통해서 sender와 receiver를 확인할 것임

- rdt1.0
	- reliable transfer over a reliable channel
	- bit error와 packet loss가 없음
	- 완벽하게 reliable한 channel을 통해서 보냄
	- sender는 단순하게 data를 packet을 만들어 보내고 receiver는 packet에서 data를 추출하기만 하면 됨
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7b7538a1-683a-43ad-ba5e-6766def3b433/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T220419Z&X-Amz-Expires=86400&X-Amz-Signature=49ece462c113819c7acc64caba67f85c24c4ba99841f8470c4890d3f63e9da2b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- rdt2.0
	- bit error가 존재함(bit가 flip될 수 있음)
	- error를 고치기 위해서 packet을 잘 받았는지 체크를 함
	- acknowledgments(ACKs)
		- receiver가 packet을 잘 받았을 경우 보냄
	- negative acknowledgements(NAKs)
		- receiver가 packet이 제대로 못 받을 경우 보냄
	- 만일 NAK을 경우 data를 다시 보냄
	- 즉 rdt2.0은 error detcetion과 ACK,NAK을 통한 msgs control을 하는 feedback의 매커니즘이 추가가 됨
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c56660e1-9024-4e75-b92a-424b0bbf9c18/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T220817Z&X-Amz-Expires=86400&X-Amz-Signature=2471f1db367659b8c4c7fcaad7da3fbceca65ae70674b7c4ae41efa579f072fb&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e77de024-f747-4356-94fd-1d7430828da8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T220849Z&X-Amz-Expires=86400&X-Amz-Signature=d26148f18ba609fc3ad242b48506172c86193ff6f82afc7a3d195c63cff74963&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/094a5730-4964-42b3-93f3-731fbb67e8f2/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T220909Z&X-Amz-Expires=86400&X-Amz-Signature=58b2dd7cf70cc4a9c6b18489439e31b91fbfc32625d99b16ff9d55bc6a909920&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 하지만 rdt2.0에서 치명적인 결함이 있음
- ACK/NAK이 잘못오게 된다면 receiver가 이 부분을 무엇인지 알 수가 없고, 이를 다시 보낼수도 없음

- rdt2.1
	- 이를 위해 rdt2.1의 경우 sender에 sequence number를 붙여 재전송인지 여부를 파악함
	- number를 통해 ACK이 깨져서 받아도 해당 packet을 다시 보내고 판단, 만일 ACK가 깨진거였다면 해당 packet을 버림
	- stop and wait
		- sender가 packet을 보내면 receiver의 response를 기다림
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0fdae945-8bc9-49e3-b2b4-441f20eba178/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T221304Z&X-Amz-Expires=86400&X-Amz-Signature=1632d4ee6714fabf0ead3e2f8f511cfa2ef2e6895eb84df3d88cd8a583c95792&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ef1daa6b-1934-4d52-9179-7e819b1a7b5a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T221340Z&X-Amz-Expires=86400&X-Amz-Signature=ba3ae9041d9160b0092ec520976d8f30be598131d037f9076d350ad4c1c49710&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- rdt2.1의 경우 sender는 sequence number를 통해서 ACK/NAK의 상태를 체크를 함
- receiver의 경우 중복체크를 확인함, ACK/NAK을 정확히 모르더라도 packet number를 통해서 체크

- rdt2.2
	- 전체적인 로직은 rdt2.1과 유사
	- NAK을 보내지 않음
	- 1번이 깨졌다면 NAK이 아닌 0번 ACK을 보냄, 1번이 깨짐을 인지함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f713f497-f5ef-4814-8e92-f9ef03239bdb/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T221855Z&X-Amz-Expires=86400&X-Amz-Signature=1a941ae1d3c42813d19dbb9c9bb31225881e37e5fc374808a63d9eae9a3bbaff&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- rdt3.0
	- packet이 아예 도착 안하면 loss를 함
	- 이에 loss를 대비해서 적당한 시간을 기다림, timer 필요
	- 기다려도 오지 않으면 timeout됨, 이를 loss로 판단하여 재전송함
	- delay가 된 경우에도 sequence number로 판단, 중복값이어도 이를 인식해서 처리함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/05ec0a69-abf2-46b9-89f0-b1a4e07c0165/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T222110Z&X-Amz-Expires=86400&X-Amz-Signature=6641f329b6d610ade75727aa773068d88ecfbc14f1397c8d368239ab48dcce76&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4e7f0f87-e5f1-4c70-abc7-c5cfd038e951/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T222140Z&X-Amz-Expires=86400&X-Amz-Signature=b052dcef0d902539b6ecc0497e25c8863e146f9ad09e6caab7f9f20c9cd7117e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8c850124-8c3c-4150-b2f8-ba0db3716bb7/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T222152Z&X-Amz-Expires=86400&X-Amz-Signature=3061b1f20d051841d712de7de50783f412b99afa6090598f497cea28a3e96621&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- rdt3.0의 performance를 생각해보면 link 사용 비율이 현저히 낮음
- 물리적인 부분에 있어서 RTT로 인해서 매우 비효율적임
- 전체비율에 비해서 기다리는 시간이 매우 김
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/52701795-9d4e-4012-8d35-a46953543513/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T222330Z&X-Amz-Expires=86400&X-Amz-Signature=0f693ae737f0d3452ddfa1f72e31e2ae1d425f75f05f7867386a4b006efbb55a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/135b53bf-f11c-40cb-93f5-8b5892844cb0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T222339Z&X-Amz-Expires=86400&X-Amz-Signature=29d2266be726b53da1835807113512e1dd410acf73c2e180d932b45d3b1162c0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- Pipelined protocols
	- 여러개를 buffering을 함, 여러개 packet을 보냄
	- 이를 통해 link 사용량을 높임, packet를 많이 보내면 그만큼 증가함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/411749b1-8cfc-46b2-86fa-38165fe57521/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T222535Z&X-Amz-Expires=86400&X-Amz-Signature=39fe3aa91ca9697abd58388ab26e94a3ada55609ce72cfcf4e869665f2c43472&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/96aedf13-107c-4bd7-bf14-b9344ea095f5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T222543Z&X-Amz-Expires=86400&X-Amz-Signature=8faef90c5adb79da571002adfc13943b9a760ceb79d6e278c9f7591e484bdab1&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- Go-Back-N
	- pipelined protocols의 일부
	- 누적된 ACK 순서대로 수신을 파악함
	- 하나의 loss가 일어나면 그 이후 data가 정상적으로 처리되더라도 loss 이전 ACK를 보냄, 그 이후 timeout으로 재전송시 loss data포함 그 이후 data를 다시 보냄
	- 재전송은 비효율적이지만 단순한 구조를 가짐

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/57d6bf26-edd6-4df3-9729-3857ef0c19cd/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T222846Z&X-Amz-Expires=86400&X-Amz-Signature=2a87c3ad667134a4c1e701f35f42b6d14ab84c4e5da3b3ad392fbe95e4669ba7&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- send_base
	- 보냈지만 ACK이 안 온 것 중 제일 오래된 것
- nextseqnum
	- 다음번에 전송할 때 확인
- ACK(n)
	- n까지 n을 포함해서 n까지 모든 packet이 잘왔음을 의미
- timeout(n)
	- ACK이 안 온 거 기준으로 retransmit, 노란색 다 보냄

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0ed38cc6-b298-4dce-96f1-2fec85c66a08/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T223059Z&X-Amz-Expires=86400&X-Amz-Signature=a69d9cb6bc96935ec15fffb5474c142eea2debe78bcea6b84c6e7b79e1a5ff42&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9c95545a-bec2-4365-acb6-0125ec7f41cd/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T223107Z&X-Amz-Expires=86400&X-Amz-Signature=526122c4a04cfd07aa4df39ff4a2c60c750d55c528befdb3179fb43b950dd398&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2ca8ed86-a316-457f-8f40-19d926982fc9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T223115Z&X-Amz-Expires=86400&X-Amz-Signature=95b588c497e7229cb5897e9d7842e9395022c278daaf1e7d9549c8fb2097638d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- Selective repeat
	- 각각 packet 별 ACK이 다름, 선택적으로 전송함
	- 이를 위해 buffering을 생각해야함, 순서대로 올리기 위해서
	- 데이터가 제대로 오지 않으면 buffer가 됨
	- 2가 loss가 일어났다면 2만을 보냄, 개별적인 timer 존재
	- 재전송이 효율적이지만 복잡한 구조임
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/91832dd0-37a4-4873-9b66-2b87b39ae5b0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T223437Z&X-Amz-Expires=86400&X-Amz-Signature=5016bf2403f92ae2f69035005faf8cff841f0883a62fc6f80d5a434768afa70b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/81e850b1-bbcf-4936-add1-0d367174441e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T223539Z&X-Amz-Expires=86400&X-Amz-Signature=9d756999c37243284a907636d37b104c86b203e76787512ececca2b41eeea432&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1b612597-ea33-4c3b-a16e-1e514319503a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T223549Z&X-Amz-Expires=86400&X-Amz-Signature=df537e6da9afb04116c4d7b97eee2e15a23fa225a006cf73faaff4ba4cce3301&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- Selective repeat이 고려해야할 사항이 있는데 window size에 따라서 packet과 sender의 상태가 어떤지 알지 못함
- 이 때문에 window size가 seq #에 비해서 절반보다는 작아야함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/07a780c1-72bc-473b-af84-49e559bc37aa/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T223738Z&X-Amz-Expires=86400&X-Amz-Signature=3011316a3be79fd3833146ce3c6120b1b08843e22f7be90f8bb43475ca237142&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
