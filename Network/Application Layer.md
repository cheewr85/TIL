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
![one](/img/Network/Applicationlayer/one.png)

- 모두 다 network application임

![two](/img/Network/Applicationlayer/two.png)

- networrk app은 network의 통신을 위한 application임
- end system에서 돌아감(network), 사용자-사용자, 서버-사용자 네트워크 통해서 통신
- 둘간의 통신, 패킷을 보내지만 network-core에서 어떻게 전달되는지 다 만들 필요없음 -> 계층화(패킷들이 어떻게 목적지로 보내야하는지 신경 쓸 필요없음) -> 알아서 보냄
- application은 end system끼리의 통신, layer를 통해 알아서 연결이 됨
- 대표적인 application 구조
	- client-server
	- peer-to-peer(P2P)
![three](/img/Network/Applicationlayer/three.png)

- server
	- 항상 켜져있음
	- 변하지않는 IP 주소
	- 데이터 센터 존재함 
- clients
	- 스마트폰등
	- 서버와 통신(필요할 때만)
	- 고객이므로 IP 주소는 바뀜
	- client끼리 통신할 수 없음

![four](/img/Network/Applicationlayer/four.png)


- Client끼리 통신
- 필요할 때 end system에서 서로 연결, 통신
- self scalability -> 그때그때 주위기기 통신, 규모가 커져도 처리를 분산시킴(server-client는 scaling을 위해 데이터센터가 존재함, 많은 사용자 처리해야하므로)
- 안정적이지 못하고 p2p 참여기기를 관리할 수 없음
- 토렌트 -> 파일 주고받은 특정 파일 여러 사용자에게 나눠 받음, 그때그때 다름, 전송 & 사용자 다름 & 사용자끼리 통신

![five](/img/Network/Applicationlayer/five.png)


- process는 program 관리단위임
	- network application 통신, process들간의 통신(컴퓨터상)
	- end system에서 실행되고 있는 program
		- client process(웹서핑 시작, 통신개시)
		- server process(상시대기)
- inter-process communication -> 같은 host에서 내부적으로 통신(컴퓨터내), OS(network 필요없음)
- message -> 서로 다른 host에 있는 process들끼리 통신을 함(네트워크 통해 message 주고 받음)
- P2P의 경우 어떤것이든 client & server가 될 수 있음

![six](/img/Network/Applicationlayer/six.png)


- message를 보내기 위한 door 역할
- process들 간의 통신을 위한 네트워크를 위한 통신을 위해 사용되는 구조를 socket이라고함

![seven](/img/Network/Applicationlayer/seven.png)


- 목적지를 어떻게 인식할지 
- host를 가지고 있음, IP주소만으로 어디로 가야할지 인식힘듬 -> port number 활용

![eight](/img/Network/Applicationlayer/eight.png)


- open protocols
	- 누구나 사용가능
- proprietary protocols
	- 앱을 통해서만 서비스 활용, 회사내에서만 제공

![nine](/img/Network/Applicationlayer/nine.png)


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
![ten](/img/Network/Applicationlayer/ten.png)
![eleven](/img/Network/Applicationlayer/eleven.png)


- application에서 아래 계층에서 지원해주기 위해 구성된 service, 요구조건에 따라서 사용

![twelve](/img/Network/Applicationlayer/twelve.png)


- application layer에서 어떤 protocol을 만든 후 service를 제공할 때, socket에서 transport layer로 내가 원하는 메시지를 밀어넣어 반대쪽 socket으로 나오게 할때 transport에서 어떤 service를 이용해서(어떤 protocol) 전송을 할것이냐를 결정해야함

## Web and HTTP
![thirteen](/img/Network/Applicationlayer/thirteen.png)
![fourteen](/img/Network/Applicationlayer/fourteen.png)
![fifteen](/img/Network/Applicationlayer/fifteen.png)

- HTTP(Hyper-Text-Transfer-Protocol)

![sixteen](/img/Network/Applicationlayer/sixteen.png)

- non-persistent HTTP
	- 지속되지 않고 매번 열고 닫고를 고려함
	- 여러개가 있다면 여러개 열림 
	- 한개의 object 보낼 때 매번 한개의 object마다 TCP Connection을 만들었다가 닫았다가 함(object마다 connection 다르게함)
- persistent HTTP
	- 한 번 열어놓으면 여러개 연결 & 유지가능

![seventeen](/img/Network/Applicationlayer/seventeen.png)
![eighteen](/img/Network/Applicationlayer/eighteen.png)

![nineteen](/img/Network/Applicationlayer/nineteen.png)


- RTT(Round-Trip-Time)
	- 한 번 갔다가 오는 시간
	- object 많으면 시간 더 걸림(non-persistent의 경우)

![twenty](/img/Network/Applicationlayer/twenty.png)


- non-persistent
	- 끊고 연결 계속 관리해야함
	- 병렬적 관리시 괜찮음
- persistent
	- connect을 열어두고 통신, response 기다리지 않고 request 여러개 보내 수신 가능
	- 하나하나 여는것보다 유용
- pipelining
	- request 여러개 보내고 각각의 response를 받음

![twentyone](/img/Network/Applicationlayer/twentyone.png)

- header lines의 경우 어떤식으로 HTTP가 작동할지 정보를 보여줌

![twentytwo](/img/Network/Applicationlayer/twentytwo.png)
![twentythree](/img/Network/Applicationlayer/twentythree.png)


- POST
	- 정보를 보내줌, server로 보냄
- URL method
	- 업로드할 정보를 담아서 보냄

![twentyfour](/img/Network/Applicationlayer/twentyfour.png)
![twentyfive](/img/Network/Applicationlayer/twentyfive.png)
![twentysix](/img/Network/Applicationlayer/twentysix.png)


- 쿠키
![twentyseven](/img/Network/Applicationlayer/twentyseven.png)


- 유저의 상태 저장 필요
- 쿠키 아이디 사용자 저장 추적가능(유저의 상태 포함)

![twentyeight](/img/Network/Applicationlayer/twentyeight.png)
![twentynine](/img/Network/Applicationlayer/twentynine.png)


## electronic mail
![thirty](/img/Network/Applicationlayer/thirty.png)


- user agent는 주로 쓰는 스마트폰 메일앱과 이메일 프로그램등을 의미함(outlook, Gmail-웹페이지에서 구성됨)
- mail server는 이메일 서로 주고받을 때 그 과정에 필요한 server임
- SMTP는 메일 서버 사이에 서로 주고받는 것임(Gmail과 Naver가 서로 메일을 주고 받을 수 있게끔)
- 메일을 보내게 되면 queue에 보낼 메일이 쌓여있음
- outgoing message queue
	- message를 담고 있는(줄 세워둠)
- user mailbox
	- 여러 유저들 존재, 각각의 유저들에게 곧 메일박스가 mail server에 존재함, 각각 다른 유저임

![thirtyone](/img/Network/Applicationlayer/thirtyone.png)


- 언제 메일이 올 지 모르기 때문에 mail server는 따로 두고 항상 켜져있음
- client - sever 구조가 형성됨 즉, 보내는 서버-받는 서버의 구조, 주고 받는 입장에서 client-server 관계가 형성됨

![thirtytwo](/img/Network/Applicationlayer/thirtytwo.png)

- 가장 믿을 만한 TCP 통신을 하고 port 25를 씀
- transfer에 있어서 3가지 phase가 있음(SMTP를 보내는데)
	- handshaking(greeting), 서로 인식(Gmail, Naver인지 서로 확인)
	- transferr of message, 내용 보냄
	- closure, 종료
- HTTP와 유사함, command 보내면 서버가 responseㅎㅁ
- 7-bit ASCII로 해야하는 제약조건이 있음

![thirtythree](/img/Network/Applicationlayer/thirtythree.png)


- mail server에 전송되는 과정
- SMTP를 통한 server 통신
- 이를 mail box에 저장, 확인함

![thirtyfour](/img/Network/Applicationlayer/thirtyfour.png)


- 끝날때까지 연결 지속
- 문자열을 활용(메시지 종류 표현)
- HTTP 
	- pull 방식, 서버에 저장된 데이터 가져오는 것이 목적(수신하는 입장에서 웹브라우저가 TCP Connection 초기화, 있는 걸 가져와 pull)
	- Command는 ASCII, body, 파일 보낼 땐 아님
- SMTP
	- 메일 보내는 입장, 보낼거라고 Client-Server에 요청(미리 읽음, mail 밀어넣어 push)
	- body까지도 ASCII, ASCII 인코딩 때문에 달라짐

![thirtyfive](/img/Network/Applicationlayer/thirtyfive.png)


- 보내지는 message에 관한 format, 안의 message를 어떻게 만들지, 원본 메일 보기를 통해 header에서 누가 어떻게 무엇을 보냈는지 알 수 있음

![thirtysix](/img/Network/Applicationlayer/thirtysix.png)


- SMTP는 항상 켜져있어 보내는데 무리가 없음
- mail access protocol 과정에서는 user agent가 원할 때 읽어야 하는 것이 다름, 여기서 어떻게 메일 박스에 접근할지 등, 이를 protocol을 활용함, 설정을 통해서 메일서버에 메일앱 이용가능(HTTP예시는 사이트에서 보는 것)

![thirtyseven](/img/Network/Applicationlayer/thirtyseven.png)


- authorization phase
	- 메일서버에 id&pw를 입력후 인증단계
- transaction phase
	- mail이 뭐 있는지, client 요구사항 반영, 종료시 명령에따라 처리됨

![thirtyeight](/img/Network/Applicationlayer/thirtyeight.png)


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
![thirtynine](/img/Network/Applicationlayer/thirtynine.png)


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

![fourty](/img/Network/Applicationlayer/fourty.png)


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

![fourtyone](/img/Network/Applicationlayer/fourtyone.png)


- 분산적 계층적으로 이루어짐
- root 기점으로 분산, 계층적으로 데이터베이스화해서 관리

![fourtytwo](/img/Network/Applicationlayer/fourtytwo.png)


- 가장 상위 계층, 최상위 Domain Server -> 다른 서버들이 모르면 질문을 함, 인증을 통해 관리

![fourtythree](/img/Network/Applicationlayer/fourtythree.png)


- authoritative의 경우 기관 책임서버로 학교, 기관 내 IP주소를 domain과 연결함

![fourtyfour](/img/Network/Applicationlayer/fourtyfour.png)


- 계층적 시스템 구조에는 포함되지 않음
- ISP, 인터넷 제공 ISP에서 원활한 제공을 위해 주로 domain name server, 인터넷 서비스 제공업체에서 IP Address를 좀 더 효율적 mapping을 위해서 제공해줌
- 매번 DNS query를 하는 것은 비효율적임, 최근 정보를 cache로 저장(바로 넘김)

![fourtyfive](/img/Network/Applicationlayer/fourtyfive.png)


- host name을 IP Address로 DNS를 활용하여 바꿈 그 방법중 하나인 반복적 쿼리
- root에게 물어보고 TLD에게 물어보고 책임 DNS에게 물어보는 식으로 반복작업
- 하지만 여기서 local DNS에 Cache가 있으면 바로 알려줌 하지만 그렇지 않는 경우 위 작업 순대로 처리해야함

![fourtysix](/img/Network/Applicationlayer/fourtysix.png)


- 재귀적 쿼리, 위와 같은 과정으로 재귀로써 타고 들어가면서 답을 얻음
- 질문을 물어본 server에게 책임을 줌 root의 부담이 커지고 반복작업과 일처리가 늘어남

![fourtyseven](/img/Network/Applicationlayer/fourtyseven.png)


- 매번 같은 반복작업은 비효율적이고 heavy함, 이를 해결하기 위해서 local에 caching을 함, 많은 사람이 요청하는 것은 local DNS server선에서 정리함, 계층적으로 부담이 줄어듬

![fourtyeight](/img/Network/Applicationlayer/fourtyeight.png)


- record 저장, 이용을 해서 IP 주소와 hostname을 mapping해 host name으로 접속이 가능함
- RR->분산적으로 저장
- type에 따라 의미하는 바가 다름

![fourtynine](/img/Network/Applicationlayer/fourtynine.png)


- 각각 query와 reply 구분, identification flags 하위의 계층에서 다양한 정보를 보낼 수 있음

## P2P applications
![fifty](/img/Network/Applicationlayer/fifty.png)

- 항상 켜있는 server가 아님
- end system이 켜져있으면 서로 통신함
- 간혈적으로 연결, 상황에 따라 바뀜

![fiftyone](/img/Network/Applicationlayer/fiftyone.png)
![fiftytwo](/img/Network/Applicationlayer/fiftytwo.png)


- 매우 큰 파일 F를 보낸다고 가정을 했을 때 server-client 구조에선 server의 한계, 제약이생김(시간이 걸림), 다운과 업로드 속도에 buttleneck이 생길 수 있음
- 두번째 사진의 식과 같이 Dc-s는 max의 해당하는 값보다는 적어도 클 것임 여기서 N 기준으로 linear하게 증가함

![fiftythree](/img/Network/Applicationlayer/fiftythree.png)


- P2P 이용시 server가 한 번만 밀어내면 됨, 그 이후로 알아서 분산적으로 하니깐(F가 어디로든 감, 여기저기 퍼짐)
- linear하게 증가하지만 똑같이 clients의 업로드 속도가 받은 만큼 올려줘야 하므로 linear하게 증가함
- Dp2p가 적어도 max값보다는 클 것임
- 근처에 똑같은 파일 공유시 P2P가 효율적 하지만 먼거리에서만 파일이 있다면 속도 문제로 Client-Server가 더 효율적일 수 있음

![fiftyfour](/img/Network/Applicationlayer/fiftyfour.png)


- Client-Server는 고정되어 있지만 P2P의 경우 분모의 업로드 속도 역시 linear하므로 Client-Server보단 증가율이 낮음(log 형태) 