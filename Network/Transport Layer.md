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
![one](/img/Network/Transportlayer/one.png)

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
![two](/img/Network/Transportlayer/two.png)

## multiplexing and demultiplexing
- multiplexing at sender
	- 여러 process별로 socket 통신이 다름
	- 여러개 socket, 어떻게 잘 취합해서 보내는지
	- socket들 간 혼선이 있으면 안됨(header를 붙임)
- demultiplexing at receiver
	- 수신입장
	- 어떤(어느)socket으로 전달해야하는지
![three](/img/Network/Transportlayer/three.png)

- Connectionless demultiplexing
	- UDP에서 사용
	- 단순하게 port nunmber를 통해서 socket 통신을 하고 port number만을 보고 해당 socket에 전달함
![four](/img/Network/Transportlayer/four.png)

- Connection-oriented demux
	- TCP에서 사용
	- TCP socket은 4개의 식별자를 사용하여 port가 같아도 다르게 보냄, 해당 process와 연결됨
![five](/img/Network/Transportlayer/five.png)

- port가 같아도 IP가 서로 다르고 그 안에도 port 번호가 달라서 수신이 다름
![six](/img/Network/Transportlayer/six.png)

- 하지만 효율성을 위해 아래와 같이 프로세스 하나 안에서 여러 소켓을 관리함
![seven](/img/Network/Transportlayer/seven.png)

## connectionless transport UDP
- UDP(User Datagram Protocol)[RFC 768]
	- best effort service
		- 즉 data를 잃을 수도 있고 순서대로 app에 전달을 하지 않을수도 있음
	- port number만 보고 연결함, 즉 둘간의 연결을 만들고 port number만 보고 처리하므로 독립적으로 적용
	- streaming multimedia, 즉 약간의 loss가 허용되는 곳에서 빨리 전달되면 활용함
	- application layer에 어느정도의 의존성 있음
![eight](/img/Network/Transportlayer/eight.png)

- checksum
	- sender에서 16-bits integers를 모두 더함
	- receiver에서 checksum을 비교해서 체크함
- wraparound 부분 기준으로 위의 두 비트를 단순하게 더함 2진수 덧셈으로 wraparound는 더해서 남는 수 이 부분을 마지막에 +1을 하여 sum으로 나타냄
- 여기서 sum과 더했을 때 모두 1이 되도록 하는 checksum을 만듬
- 이를 통해 에러 체크를 함
![nine](/img/Network/Transportlayer/nine.png)

## principles of reliable data transfer
- data를 신뢰성 있게 보내기 위해서 아래와 같은 과정이 필요함
![ten](/img/Network/Transportlayer/ten.png)

- (b)부분에서 unreliable channel을 이용하기 때문에 다양한 loss가 일어나고 reliable하지 못함
- 그렇기 때문에 reliable하게 data를 보낼 수 있는 protocol이 필요한 것이고 (b)와 같은 일련의 과정이 필요함, 데이터를 보내고 복원하는 과정이 필요

![eleven](/img/Network/Transportlayer/eleven.png)

- reliable data transfer를 위해서 위와 같은 일반적인 형태의 protocol이 있음
- rdt_send()를 통해서 reliable하게 data를 보내게끔 처리한 후
- udt_send()를 통해서 protocol에서 아래의 layer로 보게함(unreliable channel)
- 그리고 unreliable channel을 통해서 data가 전달되고 여기서 unreliable channel은 물리적인 communication channel임
- rdt_rcv()를 통해 packet이 도착했다고 보내주는 호출을 하고
- deliver_data()를 통해 수신된 packet을 활용, 상위 layer로 보내느 과정을 거침
- 위와 같은 방식으로 해야 Reliable data transfer가 가능함

![twelve](/img/Network/Transportlayer/twelve.png)

- 이를 위해 reliable data transfer(rdt) protocol의 사용과 finite state machines(FSM)을 통해서 sender와 receiver를 확인할 것임

- rdt1.0
	- reliable transfer over a reliable channel
	- bit error와 packet loss가 없음
	- 완벽하게 reliable한 channel을 통해서 보냄
	- sender는 단순하게 data를 packet을 만들어 보내고 receiver는 packet에서 data를 추출하기만 하면 됨
![thirteen](/img/Network/Transportlayer/thirteen.png)

- rdt2.0
	- bit error가 존재함(bit가 flip될 수 있음)
	- error를 고치기 위해서 packet을 잘 받았는지 체크를 함
	- acknowledgments(ACKs)
		- receiver가 packet을 잘 받았을 경우 보냄
	- negative acknowledgements(NAKs)
		- receiver가 packet이 제대로 못 받을 경우 보냄
	- 만일 NAK을 경우 data를 다시 보냄
	- 즉 rdt2.0은 error detcetion과 ACK,NAK을 통한 msgs control을 하는 feedback의 매커니즘이 추가가 됨
![fourteen](/img/Network/Transportlayer/fourteen.png)
![fifteen](/img/Network/Transportlayer/fifteen.png)
![sixteen](/img/Network/Transportlayer/sixteen.png)

- 하지만 rdt2.0에서 치명적인 결함이 있음
- ACK/NAK이 잘못오게 된다면 receiver가 이 부분을 무엇인지 알 수가 없고, 이를 다시 보낼수도 없음

- rdt2.1
	- 이를 위해 rdt2.1의 경우 sender에 sequence number를 붙여 재전송인지 여부를 파악함
	- number를 통해 ACK이 깨져서 받아도 해당 packet을 다시 보내고 판단, 만일 ACK가 깨진거였다면 해당 packet을 버림
	- stop and wait
		- sender가 packet을 보내면 receiver의 response를 기다림
![seventeen](/img/Network/Transportlayer/seventeen.png)
![eighteen](/img/Network/Transportlayer/eighteen.png)

- rdt2.1의 경우 sender는 sequence number를 통해서 ACK/NAK의 상태를 체크를 함
- receiver의 경우 중복체크를 확인함, ACK/NAK을 정확히 모르더라도 packet number를 통해서 체크

- rdt2.2
	- 전체적인 로직은 rdt2.1과 유사
	- NAK을 보내지 않음
	- 1번이 깨졌다면 NAK이 아닌 0번 ACK을 보냄, 1번이 깨짐을 인지함
![nineteen](/img/Network/Transportlayer/nineteen.png)

- rdt3.0
	- packet이 아예 도착 안하면 loss를 함
	- 이에 loss를 대비해서 적당한 시간을 기다림, timer 필요
	- 기다려도 오지 않으면 timeout됨, 이를 loss로 판단하여 재전송함
	- delay가 된 경우에도 sequence number로 판단, 중복값이어도 이를 인식해서 처리함
![twenty](/img/Network/Transportlayer/twenty.png)
![twentyone](/img/Network/Transportlayer/twentyone.png)
![twentytwo](/img/Network/Transportlayer/twentytwo.png)

- rdt3.0의 performance를 생각해보면 link 사용 비율이 현저히 낮음
- 물리적인 부분에 있어서 RTT로 인해서 매우 비효율적임
- 전체비율에 비해서 기다리는 시간이 매우 김
![twentythree](/img/Network/Transportlayer/twentythree.png)
![twentyfour](/img/Network/Transportlayer/twentyfour.png)

- Pipelined protocols
	- 여러개를 buffering을 함, 여러개 packet을 보냄
	- 이를 통해 link 사용량을 높임, packet를 많이 보내면 그만큼 증가함
![twentyfive](/img/Network/Transportlayer/twentyfive.png)
![twentysix](/img/Network/Transportlayer/twentysix.png)

- Go-Back-N
	- pipelined protocols의 일부
	- 누적된 ACK 순서대로 수신을 파악함
	- 하나의 loss가 일어나면 그 이후 data가 정상적으로 처리되더라도 loss 이전 ACK를 보냄, 그 이후 timeout으로 재전송시 loss data포함 그 이후 data를 다시 보냄
	- 재전송은 비효율적이지만 단순한 구조를 가짐

![twentyseven](/img/Network/Transportlayer/twentyseven.png)

- send_base
	- 보냈지만 ACK이 안 온 것 중 제일 오래된 것
- nextseqnum
	- 다음번에 전송할 때 확인
- ACK(n)
	- n까지 n을 포함해서 n까지 모든 packet이 잘왔음을 의미
- timeout(n)
	- ACK이 안 온 거 기준으로 retransmit, 노란색 다 보냄

![twentyeight](/img/Network/Transportlayer/twentyeight.png)
![twentynine](/img/Network/Transportlayer/twentynine.png)
![thirty](/img/Network/Transportlayer/thirty.png)

- Selective repeat
	- 각각 packet 별 ACK이 다름, 선택적으로 전송함
	- 이를 위해 buffering을 생각해야함, 순서대로 올리기 위해서
	- 데이터가 제대로 오지 않으면 buffer가 됨
	- 2가 loss가 일어났다면 2만을 보냄, 개별적인 timer 존재
	- 재전송이 효율적이지만 복잡한 구조임
![thirtyone](/img/Network/Transportlayer/thirtyone.png)
![thirtytwo](/img/Network/Transportlayer/thirtytwo.png)
![thirtythree](/img/Network/Transportlayer/thirtythree.png)

- Selective repeat이 고려해야할 사항이 있는데 window size에 따라서 packet과 sender의 상태가 어떤지 알지 못함
- 이 때문에 window size가 seq #에 비해서 절반보다는 작아야함
![thirtyfour](/img/Network/Transportlayer/thirtyfour.png)

## connection-oriented transport TCP
- TCP
	- point-to-point
		- 하나의 sender에 하나의 receiver
	- reliable, in-order byte stream
	- pipelined
	- full duplex data
		- 양방향 통신을 함(bi-directional data)
	- connection-oriented
		- handshaking
	- flow controlled 
![thirtyfive](/img/Network/Transportlayer/thirtyfive.png)
![thirtysix](/img/Network/Transportlayer/thirtysix.png)
![thirtyseven](/img/Network/Transportlayer/thirtyseven.png)

- TCP round trip time, timeout
	- TCP Timeout에 있어서 적당한 시간이 필요함
	- 이를 위해서 RTT를 직접 재서 처리를 함

- TCP reliable data transfer(rdt)
![thirtyeight](/img/Network/Transportlayer/thirtyeight.png)
![thirtynine](/img/Network/Transportlayer/thirtynine.png)
![fourty](/img/Network/Transportlayer/fourty.png)
![fourty](/img/Network/Transportlayer/fourtyone.png)
![fourtytwo](/img/Network/Transportlayer/fourtytwo.png)

- TCP ACK generation
	- 만일 모든 data가 expected한 seq #로 in-order하게 보내진다면, 우선 ACK을 바로 보내지 않고 기다렸다가 보냄
	- in-order segment로 보냈지만 ACK이 안 간 것이 있다면 그 즉시 마지막에 수신한 ACK을 보냄
	- 제대로 된 순서로 segment가 보내지지 않았다면, ACK을 duplicate해서 보냄
	- 만일 gap이 발생한다면 그에 해당하는 ACK을 바로 보냄, 즉 gap 발생시 duplicate ACK을 보냄
![fourtythree](/img/Network/Transportlayer/fourtythree.png)
![fourtyfour](/img/Network/Transportlayer/fourtyfour.png)

- TCP flow control
	- receiver가 sender를 컨트롤함, 오버플로우가 나지 않게 하기 위해서
	- 이를 위해서 buffer를 활용, buffer의 남은 양 추가해서 보내어 이를 통해 오버플로우가 나지 않도록 보내는 양을 조절하게끔 할 수 있음
![fourtyfive](/img/Network/Transportlayer/fourtyfive.png)
![fourtysix](/img/Network/Transportlayer/fourtysix.png)

- Connection Management
	- handshake 즉, 서로간 데이터 전송을 약속해야 데이터를 서로 주고 받음
- 2-way handshake
	- connection을 만들고 서로 인식한 뒤 보냄
	- 하지만 loss 발생시 신뢰성 있게 동작했는지 모름
![fourtyseven](/img/Network/Transportlayer/fourtyseven.png)
![fourtyeight](/img/Network/Transportlayer/fourtyeight.png)

- 3-way handshake
	- 2-way와 비슷하지만 한 번 더 확인 message를 보냄, 연결을 확실히 확인함
	- 한 번의 전송으로 끝나지 않고 request에 대한 ACK이 정상적으로 받았는지 도착했는지 확인 후 connection을 열음
![fourtynine](/img/Network/Transportlayer/fourtynine.png)
![fifty](/img/Network/Transportlayer/fifty.png)

- 여기서 connection을 닫는 과정에서도 연결종료요청을 바탕으로 server에서 더 이상 보낼 것이 없으면 연결종료확인을 보낸 뒤 연결종료를 알림, 그러고 ACK을 보내고 연결종료를 함
- 서로 보낼 것이 없음이 확실하면 닫음
![fiftyone](/img/Network/Transportlayer/fiftyone.png)

## principles of congestion control
- 여기서의 혼잡제어는 flow control과 다름
- network 혼잡도 제어를 하는 것임
- network 혼잡시 packets를 loss하거나 delays가 매우 긴 상황이 발생하기 때문임
- 기본적인 케이스는 아래와 같음(buffer가 무한대일 경우, 재전송도 없음)
	- Router에서 보내는 속도를 R이라고 할 때 최대 throughput이 R/2이고 그 전까지는 처리에 문제가 없지만 R/2에 근버할수록 delay가 매우 커짐
	- 그 값이 R/2보다 커질 순 없음
![fiftytwo](/img/Network/Transportlayer/fiftytwo.png)

- 두번째는 finite한 buffer가 있고 retransmit을 하게 되는 경우
- retransmit까지 있으므로 기존의 in의 값보다 더 큰 값을 전송함
![fiftythree](/img/Network/Transportlayer/fiftythree.png)

- 이상적인 상황 즉, buffer가 비었을 때만 보내는 경우 아래와 같음
![fiftyfour](/img/Network/Transportlayer/fiftyfour.png)

- 그리고 loss를 안는 상황의 경우, 즉 loss가 났을 때만 재전송을 하는 케이스는 아래와 같음
- 그래프가 재전송만큼 손해를 보지만 큰 성능손해는 없음
![fiftyfive](/img/Network/Transportlayer/fiftyfive.png)
![fiftysix](/img/Network/Transportlayer/fiftysix.png)

- 실제론 timeout에 의한 copy를 하게 될 경우, copy로 인해서 다시 재전송, 손실 발생 효율이 떨어짐, 쓸데없는 낭비가 생김
![fiftyseven](/img/Network/Transportlayer/fiftyseven.png)
![fiftyeight](/img/Network/Transportlayer/fiftyeight.png)

- 하나의 router가 아닌 여러개의 router와 host가 아래와 같이 연결되어있을 경우 만일 Host A의 빨간색이 병목현상이 발생하면 Host D의 파란색은 계속 loss가 생기고 throughput은 0으로 됨
- 서로 영향을 미치고 병목현상에 의한 loss 발생시 전송만 냅다하는 악순환이 생김
- 이를 해결하기 위해서는 속도조절을 하는것이 기본적임
![fiftynine](/img/Network/Transportlayer/fiftynine.png)
![sixty](/img/Network/Transportlayer/sixty.png)

## TCP congestion control
- congestion control을 위해서 loss가 안나면 전송을 2배씩 계속 증가시키지만 loss가 나면 cwnd를 절반으로 줄임, linear하게 증가시킴
![sixtyone](/img/Network/Transportlayer/sixtyone.png)

- cwnd는 노란색 부분을 넘을 수 없음(cwnd -> congestion window), rate는 추정치
![sixtytwo](/img/Network/Transportlayer/sixtytwo.png)

- slow start
	- start만 slow하게 함
	- 처음에는 1MSS였지만 2배로 계속해서 늘림, ssthresh, 즉 혼잡회피를 위한 값에서 도달했을 때 혼잡이 예상되면 그 속도를 1씩만 증가, 즉 linear하게 늘림
![sixtythree](/img/Network/Transportlayer/sixtythree.png)

- 여기서 처리방법에 있어서 RENO와 Tahoe의 차이가 있음
	- Tahoe는 timeout, duplicate 상황에서의 congestion 예상시 window를 1로 시작을 함
	- Reno의 경우는 duplicate시에 절반으로 줄인 값을 시작으로 linear하게 증가시킴, fast recovery라고도 함, timeout에서는 1부터 시작함
![sixtyfour](/img/Network/Transportlayer/sixtyfour.png)
![sixtyfive](/img/Network/Transportlayer/sixtyfive.png)
![sixtysix](/img/Network/Transportlayer/sixtysix.png)
