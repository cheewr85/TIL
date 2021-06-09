## Bus & I/O

## Roadmap
- [시스템버스](#시스템버스)
- [I/O 전송](#I/O-전송)
- [I/O 버스](#I/O-버스)
- [버스 사이클](#버스-사이클)
- [인터럽트](#인터럽트)

## 시스템 버스
- 메모리버스, 전면버스(Front Side Bus, FSB), 호스트 버스라고도 부름 
	- CPU의 내부와 외부를 연결하는 것이 주요 목적
	- CPU, 메인메모리, 칩셋 사이의 정보 교환 통로
	- 주로 CPU와 메인메모리 사이의 메모리버스, 메인메모리는 주로 메모리 컨트롤러보다 시스템버스에 직접 동기 되도록 설계
- 입출력 버스, I/O 버스
	- I/O 컨트롤러와 입출력장치 사이의 버스
	- 시스템 버스에서 갈라져 나와 다양한 입출력장치 연결

![one](/img/ComputerStructure/Systembus/one.png)

- 멀티프로세스 구조에서 로컬버스와 시스템버스
	- 로컬 버스 : 각 로컬 프로세서를 중심으로 연결되는 버스
- 시스템버스
	- 각 프로세스 간의 중재 역할을 담당하는 공통 버스
	- 주로 버스 컨트롤러와 공유 메모리 사이를 연결
- 단일 CPU 구조에서도 로컬버스의 개념이 존재
	- 메인보드의 CPU가 가장 강력한 메인 프로세서
	- 그 외 비디오 카드, 네트워크 카드, 키보드 등 각종 I/O 컨트롤러도 각자의 로컬 프로세서
		- 로컬 프로세서 자신만이 사용하는 로컬버스 존재

- 인텔 터보 부스터 기술
	- 멀티코어 프로세서에서 일부 코어의 동작 클럭만 순간순간 동적으로 끌어 올려주는 기술
	- 코어를 다 쓰지 않을 경우 운영체제가 CPU에 요청, 발열이나 전기적인 한계에 도달하면 자동으로 내림
	- 아래와 같이 계산할 수 있음

![one](/img/ComputerStructure/Systembus/two.png)
![one](/img/ComputerStructure/Systembus/three.png)

## I/O 전송
- 메모리와 I/O 장치를 주소로 구분
	- CPU가 하드웨어를 정확하게 제어하기 위함
		- 메모리 주소 : 주로 반도체 메모리에 할당
		- I/O 주소 : 반도체 메모리를 제외한 나머지
	- 대개 한 주소에 한 바이트를 할당
- 어드레스 맵(address map)
	- 메모리 주소나 I/O 주소의 범위와 용도를 알기 쉽도록 지도와 같이 세밀한 그림이나 표로 정리한 자료
		- 메모리 맵(memory map)
		- I/O 맵(I/O map)

![one](/img/ComputerStructure/Systembus/four.png)

- I/O 전송방식
	- 입출력장치를 효율적으로 관리하기 위한 방법
		- CPU는 하나지만 빠르고 I/O 장치는 종류는 많고 느림
		- I/O 전송방식을 효율적으로 설계하면, CPU가 입출력장치를 관리하는 시간을 절약

![one](/img/ComputerStructure/Systembus/five.png)
![one](/img/ComputerStructure/Systembus/six.png)

- 폴링방식
	- 혹은 프로그램에 의한 I/O 전송방식
	- CPU가 주기적으로 각 I/O 장치의 상태를 검사해 전송할 데이터가 있으면 이를 처리하는 방식
		- 특정 I/O 주소들을 순서대로 지정해 일정한 시간 간격으로 매번 액세스하도록 프로그래밍
		- 폴링(polling) : 특정 주소를 지정해 그 주소에서 데이터를 내놓도록 권유해 이를 가져오는 과정
	- 구조가 간단하나 CPU 입장에서는 비능률적
		- 언제 일어날지 모를 데이터 전송에 대비해 I/O 장치를 검사하는 반복 루프를 계속 돌려야 하므로 시간 낭비(100주소 x 100회 = 초당 10000번)
- 인터럽트 방식
	- 혹은 인터럽트에 의한 I/O 전송방식 
	- I/O 장치의 데이터 전송 요청이 들어올 때만 CPU가 이를 처리하는 방식
		- 전송할 데이터가 있을 때 CPU에 인터럽트 서비스 요청
		- CPU는 일을 멈추고 요청한 데이터의 전송에 관여
		- 요청한 작업이 끝나면 CPU는 본래 하던 일로 복귀
	- 인터럽트 방식에 의한 I/O 데이터 전송 사례
		- 마우스나 키보드에 입력이 있을 때 
		- 프린터에 인쇄할 준비가 되어있을 때
		- 모뎀에 송신 준비가 되거나 수신 데이터가 있을 때

![one](/img/ComputerStructure/Systembus/seven.png)

- CPU 점유율
	- I/O 전송방식이 컴퓨터시스템의 성능에 얼마나 부담을 주는지 처리 성능을 비교할 기준으로 필요
	- 주변장치의 데이터 전송 요청이 들어오면 이를 처리하기 위해 CPU가 얼마나 시간을 할당하는지 표시 
	- CPU 점유율 = 초당 필요 클럭 수 / 초당 CPU 클럭 수 x 100%
- 이 관점으로 아래와 같이 폴링방식과 인터럽트 방식의 부담이 있음

![one](/img/ComputerStructure/Systembus/eight.png)
![one](/img/ComputerStructure/Systembus/nine.png)
![one](/img/ComputerStructure/Systembus/ten.png)

- DMA(Direct Memory Access) 방식
	- 직접 메모리 액세스, 메모리와 I/O 장치 사이의 데이터 전송을 CPU 대신 별도의 DMA 컨트롤러가 담당하는 전송방식

![one](/img/ComputerStructure/Systembus/eleven.png)

- DMA 컨트롤러는 CPU와 독립적으로 데이터를 전송
	- DMA 컨트롤러가 CPU에게 버스 사용권을 요구하면 CPU가 이를 승인하도록 설계
	- DMA 채널 설정 이후 DMA 컨트롤러가 데이터를 전송하는 동안 CPU가 관여하지 않음
		- 폴링과 인터럽트 방식 -> CPU가 데이터 전송에 직접 개입, 읽기와 쓰기 과정에 데이터가 반드시 CPU를 거처야
- DMA 채널 설정 -> CPU가 DMA 컨트롤러에 데이터 전송을 의뢰할 때 다음 정보를 넘겨주어야
	- 데이터가 출발할 메모리나 I/O 장치의 시작 주소
	- 데이터가 도착할 메모리나 I/O 장치의 시작 주소
	- 전송될 데이터 블록의 크기
- DMA 동작 모드
	- CPU가 버스를 사용하지 않는 시간에 데이터를 전송
		- DMA 컨트롤러가 시스템버스, I/O 버스를 직접 액세스
	- 사이클 스틸링 모드(cycle stealing mode) DMA
		- CPU가 메모리 등의 시스템 자원을 사용하지 않는 대기 상태나 내부 동작 중일 때, 마치 CPU 버스 사이클을 훔치듯 그때그때 데이터를 전송하는 방식
	- 버스트 모드(burst mode) DMA
		- 데이터의 전송방향을 먼저 정하고 한 번에 많은 양의 데이터를 집중적으로 내보내는 방식
		- 둑이 터지듯 다량의 데이터가 한꺼번에 전송
- 아래와 같이 부담이 있을수 있음

![one](/img/ComputerStructure/Systembus/twleve.png)

## I/O 버스
- I/O 버스는 시스템버스에서 갈라져 나옴
	- 인터페이스 방법과 속도가 다양한 주변장치들을 연결하므로 CPU와 주로 비동기로 동작

![one](/img/ComputerStructure/Systembus/thirteen.png)

- 그래픽 어댑터는 I/O 장치 중 특히 고속을 목표
	- I/O 버스 전체가 아닌 그래픽 전용 채널을 분리

![one](/img/ComputerStructure/Systembus/fourteen.png)

- VESA 로컬 방식
	- 16비트 ISA 슬롯에 커넥터를 추가해 32비트로 개선
	- 시스템버스에 I/O 버스가 동기되어 부하 걸림 
- 나중에 32비트 I/O 버스는 인텔의 PCI 방식이 주도
	- 범용 I/O 버스 전체를 고속으로 설계하는 것은 한계
	- 효과적인 방법은 그래픽 전용 채널을 분리하는 것 
- AGP(Accelerated graphics port)
	- PCI 버스 기반으로 구현된 일종의 그래픽 전용 포트
	- 이후의 그래픽 전용 버스는 대개 고속 슬롯으로 분리해 독점적으로 I/O 버스를 사용하도록 설계
- PCI(Peripheral Component Interconnect)
	- 인텔이 설계한 지능적인 I/O 버스
	- 주변장치를 자동으로 인식하는 PnP 기능이 가능
	- 버스 자체가 일종의 버퍼 역할
		- PCI 버스에 연결된 장치들은 CPU와 비동기로 동작 
		- CPU와 주변장치 사이의 데이터 전송에서 I/O 버스 컨트롤러가 마치 독립적인 프로세서처럼 동작
	- 과거의 ISA 버스와도 호환
		- ISA 버스의 신호들과 IRQ 신호를 생성
	- 병렬인 PCI 버스는 직렬인 PCI-E 버스에 대체됨
- PCI 익스프레스(PCI express, PCI-E)
	- PCI와 달리 전혀 새롭게 설계한 고속 시리얼 버스
	- 전송채널로 독립적인 선로 사용
		- 각 채널이 간섭 없이 독립적인 전송속도를 확보, 선로당 송수신의 2개 단방향선으로 하나의 전송채널 구성
	- 전송채널 개수를 늘려 간단히 전송속도 높임
		- x1, x16, x32 배속 등으로 데이터 전송속도 표시
		- PCI-E 3.0 x16 링크 -> 약 1GB/s x 16배속 = 16GB/s
	- PCI-E 버스와 확장카드 개선 표준(표 7.2)
		- PCI-E 3.0, 4.0은 128b/130b 인코딩 방식, 오버헤드를 제외한 약 98.5%가 실제 데이터 전송속도
- 요즘 I/O 버스 방식의 주류는 PCI에서 PCI-E처럼 패럴렐에서 시리얼 방식으로 바뀜

![one](/img/ComputerStructure/Systembus/fifteen.png)
![one](/img/ComputerStructure/Systembus/sixteen.png)

- USB 인터페이스
![one](/img/ComputerStructure/Systembus/seventeen.png)

- IEEE 1394
![one](/img/ComputerStructure/Systembus/eighteen.png)

- 썬더볼트
![one](/img/ComputerStructure/Systembus/nineteen.png)

- I/O 버스의 연장
![one](/img/ComputerStructure/Systembus/twenty.png)

- 확장카드나 주변장치가 컴퓨터에 연결되려면 I/O 버스를 연장해 입출력 신호의 통로를 만들어야
	- I/O 버스 컨트롤러와 운영체제가 지원해 주어야
	- 연장되는 방법에 따라 -> 본체 내부와 외부 I/O 장치
- 내부 I/O 장치
	- I/O 확장 슬롯에 연결되는 추가 확장카드
	- I/O 커넥터에 연결되는 내장 드라이브 등
- 외부 I/O 장치
	- 유선이나 무선 I/O 포트에 연결되는 각종 주변장치들

- I/O 확장 슬롯
	- 메인보드에 추가 어댑터를 꽂도록 확장시키니 I/O 버스의 연장, 줄여서 I/O 슬롯 
	- 시스템보드 상에 위치하며 커넥터 형태
		- 추가 확장카드를 설계할 수 있도록 I/O 주소버스, I/O 데이터버스, I/O 제어버스가 범용으로 연장
	- 시스템보드 설계에 따라 슬롯의 종류와 개수 다름
		- 과거에 설계된 느리고 자주 충돌하고 많은 면적을 차지하던 확장 슬롯들은 하나씩 제거됨

![one](/img/ComputerStructure/Systembus/twentyone.png)

- I/O 커넥터
	- 컴퓨터 본체 내부에서 HDD나 ODD같은 입출력장치들을 위한 접합부로 필요
		- 내장형 드라이브와 LED 램프 등 각종 I/O 장치들은 I/O 커넥터를 통해 시스템보드에 케이블 선으로 연결
	- 범용으로 설계되지 못하고 해당 커넥터에 맞는 인터페이스 규격을 사용해야

![one](/img/ComputerStructure/Systembus/twentytwo.png)

- I/O 포트
	- 주변장치를 연결하는 I/O 데이터의 출입구
	- 컴퓨터시스템이 주변장치나 네트워크 회선과 자료를 주고받기위해 컴퓨터 본체 외벽에 설치한 접합부
		- 접속 케이블을 꽂을 수 있도록 본체 외벽에 출구를 만들고 내부적으로는 시스템보드에 연결
		- 범용으로 설계되지 못하고 해당 I/O 포트에 맞는 인터페이스 규격을 사용해야

![one](/img/ComputerStructure/Systembus/twentythree.png)
![one](/img/ComputerStructure/Systembus/twentyfour.png)

## 버스 사이클
- 버스를 이용해 메모리나 I/O 장치에서 데이터를 읽거나 쓰기위해 반복적으로 수행해야 하는 일련의 연속동작
- CPU의 데이터 전송은 버스 사이클 단위
	- 메모리버스 사이클 -> 기억장치를 구동
	- I/O 버스 사이클 -> 입출력장치를 구동
- 로컬버스에서 동작발생 시간을 설계하는 방법
	- 동기식 버스 -> 시스템버스 클럭에 동기되어 동작결정
	- 비동기식 버스 -> 다른 신호의 발생 여부로 동작결정
- 동기식버스

![one](/img/ComputerStructure/Systembus/twentyfive.png)

- 비동기식 버스

![one](/img/ComputerStructure/Systembus/twentysix.png)

## 인터럽트
- 하드웨어나 소프트웨어가 즉시 주목할 사건이 일어났을 때 프로세서에게 경보를 알리는 신호
	- 작업 중단을 요구하는 우선순위가 매우 높은 통지
- 인터럽트가 발생하면 현재 작업 상태를 저장하고 해당 인터럽트 핸들러 프로그램을 실행
	- 인터럽트 서비스 루틴(ISR)이라고도 함
- 인터럽트 벡터(interrupt vector) 테이블
	- 메인메모리의 특정 영역에 자리해 각 인터럽트 요청에 대한 인터럽트 핸들러의 시작 주소들을 저장
- 인터럽트 폭풍(interrupt storm)
	- 인터럽트 처리 시간이 과도해 시스템 성능에 심각하게 방해주는 현상

- 오리지널 IBM PC의 인터럽트

![one](/img/ComputerStructure/Systembus/twentyseven.png)

- 하드웨어 인터럽트
	- 정전 등 하드웨어적인 문제, 입출력장치의 데이터 전송 요청, 타이머 종료, 프로세서 간 통신 등에서 발생
	- 각 I/O 장치와 인터럽트 컨트롤러가 연결되는 고유 IRQ 선이 필요 -> 하드웨어 인터럽트의 개수는 프로세서에 연결되는 IRQ 선의 개수에 제한
	- 주로 CPU 외부 장치의 요청에 의해 발생, 외부 장치에서 일어나는 사건은 언제 일어날지 모르기 때문에 프로세서의 시간 낭비를 피하는 방법으로 도입
	- CPU 내부에 인터럽트 마스크 비트를 설정해 외부 하드웨어 인터럽트를 무시할 수 있도록 설계
		- 막을 수 있는 인터럽트(maskable interrupt) : IRQ 사용
		- 막을 수 없는 인터럽트(non-maskable interrupt, NMI)
			- 우선순위가 가장 높은 절대 무시될 수 없는 인터럽트
			- 하드웨어 에러에서 발생하거나 CPU의 심각한 오동작을 방지하기 위해 일부러 발생시킴 -> 전원장치 실패 인터럽트나 타임아웃 인터럽트에 따른 CPU 리셋이 대표적
- 소프트웨어 인터럽트
	- 프로그램 명령 수행에 오류가 발생한 경우, 프로그램 사용자의 의도로 시스템을 호출한 경우 등에서 발생
	- 물리적인 선이 필요 없어 수백 개를 사용
	- 주로 CPU 내부 명령의 실행에 의해 발생
		- 프로세서 자체의 예외적인 조건에 의하거나, 함정 또는 예외(exception) -> divide-by-zero 발생
		- 일련의 특별한 명령어에 의해 발생
	- 사용자 의도로 운영체제를 호출하는 경우
		- 응용프로그램이 필요할 때 BIOS나 디바이스 드라이버 같은 OS 수준에서 수행이 가능한 서비스를 요구
		- 디스크에 데이터를 쓰거나 읽으려면 디스크 컨트롤러와 통신하기 위해 소프트웨어 인터럽트를 사용
		- 일종의 감시자 호출(Supervisor call, SVC)
			- 사용자 의도로 OS 서비스를 원하는 소프트웨어 요구

- 인터럽트 제어 신호
	- 인터럽트 요청(interrupt request, IRQ) 신호
		- 인터럽트 발생시 I/O 장치가 CPU에 버스 사용을 요청
	- 인터럽트 확인(interrupt acknowledge, INTA) 신호
		- CPU가 외부 장치에 인터럽트 요청 접수를 알림
	- 인터럽트 컨트롤러는 CPU와 입출력장치 간에 비동기적인 데이터 전송을 지원, 버스 사용권을 조정
		- 인터럽트를 사용하는 I/O 장치가 전송 준비가 되면 CPU측에 IRQ신호를 보내 데이터 전송을 요구
		- CPU는 전송을 요구한 장치를 조사, 이 장치를 위해 I/O 버스를 사용하고 INTA 신호를 보내 IRQ를 클리어
- 예시
![one](/img/ComputerStructure/Systembus/twentyeight.png)

