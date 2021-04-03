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
