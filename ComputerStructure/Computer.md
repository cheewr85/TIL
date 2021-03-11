## Computer

## Roadmap
- [컴퓨터 시스템](#컴퓨터-시스템)
- [컴퓨터의 발달](#컴퓨터의-발달)
- [개인용 컴퓨터](#개인용-컴퓨터)
- [컴퓨터의 분류](#컴퓨터의-분류)
- [정보의 표현](#정보의-표현)

## 컴퓨터 시스템
- 컴퓨터와 OS의 구조
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c411d89a-1c93-4101-8fd8-d24078a7fe34/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T014421Z&X-Amz-Expires=86400&X-Amz-Signature=7b54e51a117a197971483ef08253e80bb0c5b09a8d325a324dd985a722492e39&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- S/W 계층구조
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/20c5f0cb-319c-44d2-b153-f0ea1ba7a2ee/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T014512Z&X-Amz-Expires=86400&X-Amz-Signature=ad49890e8e886759623c8dad15c9e597c2463509ceb6ba3f3c65ae06435f97b5&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 컴퓨터라는 어원 자체는 <계산하는 사람>에서 출발(compute)
- 일반적 정의 : 외부 프로그램이나 데이터 입력을 받아들여 내부 전자회로에서 자료를 계산하거나 처리해 정보를 저장하고 결과를 출력하는 기계
- 에니악(ENIAC, 1946)
	- 최초의 전자식 프로그래머블 컴퓨터
	- 배선작업을 이용
- 에드삭(EDSAC, 1949)
	- 최초의 프로그램 내장방식(Storage, 저장-메모리)
- 기본 구성
	- 하드웨어 요소
		- 중앙처리장치(CPU-Central Processing Unit), 기억장치(Memory), 입출력장치(I/O Device)
		- 쉽게 고치거나 수정 할 수 없음
	- 시스템 소프트웨어 요소
		- 하드웨어 구동과 관련된 프로그램들의 집합(Device Driver, 부팅 프로그램, 펌웨어, 운영체제)
- 하드웨어와 소프트웨어
	- 하드웨어(Hardware)
		- 내부적인 동작을 담당하는 물리적 기계 장치(고치기(수정) 쉽지 않음)
		- 전자 부품, 각종 보드, 주변장치와 기계 설비
		- 정보가 처리되는 물리적 장치와 정보의 전송경로
	- 소프트웨어(Software) = 프로그램(program)
		- 외부적인 운영을 담당하는 논리적인 명령어(program)들의 집합(유연함, 고치기 쉬움)
		- 컴퓨터가 인식할 수 있는 언어로 작성된 시스템 프로그램과 사용자 편의를 위해 만들어진 응용프로그램 
		- 프로그래밍 언어로 작성된 명령어 리스트 
		- 순서에 따라 수행해야 할 작업들의 절차
- 수정하기 어려운 정도에 따라
	- 하드웨어 > 펌웨어 > 소프트웨어
	- 펌웨어(Firmware)
		- BIOS(Basic Input Output System)
			- 기본적으로 있는 소프트웨어(Device 제어)
			- 마더보드(ROM에 저장됨) -> 기계를 통한 프로그래밍
			- ROM(Read Only Memory) : 기계 이용 프로그래밍, 읽는 용도
			- 하드웨어 세팅 가능
		- 하드웨어와 소프트웨어의 중간 성질
		- 하드웨어를 정확하게 제어해주는 프로그램들의 집합

## 컴퓨터의 발달
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/937f6324-9578-489e-bc68-6a0d5828063d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T015639Z&X-Amz-Expires=86400&X-Amz-Signature=6344901b2989b2f08fa29715a474cbecef2e6121c596414d6d01793100c64044&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/998071c8-b248-4a06-b163-be2130905ce5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T015710Z&X-Amz-Expires=86400&X-Amz-Signature=05c7f8595ad7655289b13381a6cd11a6c6ee354b9d40b9e3a3ab92e7fb67c808&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 진공관, 외부배선 사용은 트랜지스터를 활용함
- 1953년 이후 PC크기는 작아지고 기술의 발달로 micro processor까지 활용을 함

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/39aa06a7-dea0-470e-a8a5-a2fbec411a6f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T015910Z&X-Amz-Expires=86400&X-Amz-Signature=980c0d14ba1d4e98f2af3983a655fc99135d36c7df63e8c3789d4535bcd9a16c&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 전기기계식 컴퓨터의 원리, 트랜지스터와 비슷
- 전류가 흐르면 접점이 기계적으로 전자석이 달라붙음
- 기계적인 스위칭으로 2진법 표현, 여러개를 모아 논리연산 사칙연산등 구현

- Grace M.Hopper
	- 컴파일러 개발 : 프로그램을 짜면 프로그램 돌아가도록 컴파일하는 기능
		- 원시적인 인터프리터(해석 1:1 매칭)
	- 버그(bug) 발견
		- 프로그램에서 부정확한 결과나 충돌을 일으키는 오류나 결함
	- 디버그(debug) 혹은 디버깅(debugging)
		- 프로그램에서 코딩 오류를 찾아 수정하는 과정

- 튜링머신(Turing Machine)
	- 무한대 저장용량과 고장 없는 일종의 가상 기계
	- 현대적인 컴퓨터에 대한 수학적 모델 
- 튜링테스트(Turing test)
	- 컴퓨터가 얼마나 사람과 비슷하게 대화할 수 있는지 판단해 인공지능을 갖는 정도를 판정

- Maurice Wilkes
	- 어셈블리 언어 : 컴퓨터가 알아듣는 기계언어보다 상위언어(기계어와 가깝지만 사람이 알아볼수도 있는 정도)
	- 서브루틴 라이브러리 고안

- 폰 노이만 구조
	- 현대적인 컴퓨터의 개념, 프로그램 내장방식과 순차 실행
	- 전자계산기에 기억장치를 갖추고 연산 순서를 부호화해 기억시킨 후 기억된 내용을 순차적으로 꺼내 명령을 해독하고 연산을 실행함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b5ea972b-c468-4baa-8188-2cbfd35a7f17/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T020715Z&X-Amz-Expires=86400&X-Amz-Signature=279ac2faf538d20bc54ec4a75d39f9c9503961e274952bfa983a32c4e8a7d445&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- Control Unit
	- 프로그래밍의 실행관련 부분을 해석하고 컨트롤(for문을 보고 반복을 하던가, 연산을 하는 것)
	- 코딩된 문장을 가져다가 해석, 실행, Program Memory에서 일부를 순서대로 하나씩 가져와 Program 해석
- Arithmetic/Logic Unit
	- 순수하게 계산하는 Unit(데이터 필요, Data Memory)
- Data Memory
	- 하나로 써서 주소를 주고 데이터 만듬
- IAS 컴퓨터(현대컴퓨터와 유사)
	- 주기억장치, 산술논리 연산장치, 프로그램 제어장치 ,입출력 장치로 구성
	- 기억장치에 저장된 순서대로 실행
	- 전송, 분기, 산술 및 논리 등 명령어 타입(분류)
	- 제어장치와 연산장치에 각종 레지스터들 포함 
		- 레지스터 : CPU안에 내장되어 용량이 크지 않음, CPU와 근접해 있어 메모리 액세스 속도 빠름, 임시 저장용
	- 명령어 인출과 실행 사이클을 반복적으로 수행

## 개인용 컴퓨터
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/60576c33-4267-4478-a487-6e666226ed03/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T021551Z&X-Amz-Expires=86400&X-Amz-Signature=6602c434daf8ece0444f250c08ff7581947918335f8e94d7bceb6d6395d3a977&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6299d6de-5638-441b-bd40-7728af7003fa/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T021625Z&X-Amz-Expires=86400&X-Amz-Signature=65174eb9f00f4c31604877e6387e21da8bfd0cfbf5896b1aae1e96c22183206e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- CPU -> 메모리(데이터 저장)
	- Address Bus + Data Bus(메모리에 저장) 동시에 씀
- Address Bus
	- CPU -> 메모리(주소 인식 -> 데이터 전달) -> Data Bus(메모리 -> CPU)
- 여기서 wires는 bit임
- Register
	- CPU 안에 있는 메모리(속도가 빠르나 용량이 적음)
	- 데이터 저장 교환함
	- CPU-register가 몇 bit로 데이터를 주고받느냐에 따라 컴퓨터 bit 결정
- 위 컴퓨터는 데이터를 8 bits로 주고 받으므로 8 bit 컴퓨터
- 우선순위는 register - CPU의 데이터 bit 관계임
- GUI 시스템 -> 마우스를 움직이고 아이콘을 선택하는 등, 타이핑을 하지 않고 상호작용함

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2317a383-2f4f-4ab1-adba-79f27ac8d173/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T022127Z&X-Amz-Expires=86400&X-Amz-Signature=55e2e30b5d749262d16a5a004ba469e0dfdac2a4c6e6af4ded19f26b8c60ad0f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

## 컴퓨터의 분류
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1990a063-458e-4b97-ac79-bb88bc09a8b6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T022411Z&X-Amz-Expires=86400&X-Amz-Signature=dda9ee1b97905b7c625d55f5d39e77d3817f48c8a14f17e3f5c9c08afb48e0d2&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 컴퓨터의 세대
- 1세대 컴퓨터
	- 진공관 소자 사용
	- 주로 기계어로 프로그래밍(숫자나 그에 매칭되는 간단한 명령어, 최적화 되어 있지 않음)
- 2세대 컴퓨터 
	- 트랜지스터 같은 반도체 소자 사용
	- 포트란, 코볼 등 고급 프로그래밍 언어 개발
	- 원격 데이터 통신, 운영체제(O/S), 다중작업(multi-tasking)등의 개념 도입
- 3세대 컴퓨터 
	- 집적회로(IC) 사용
	- 다중작업, 실시간처리(realtime), 시분할 시스템(time division), 사용자 프로그램등의 체계가 확립
- 4세대 컴퓨터 
	- 마이크로프로세서가 CPU로 개발되어 사용
- 5세대 컴퓨터
	- 차세대 컴퓨터 연구, 초병렬 컴퓨터, 웨어러블 컴퓨터 등

- 처리 능력에 따른 분류
- 소형 컴퓨터(마이크로컴퓨터)
	- 개인용 컴퓨터와 전문가용 워크스테이션
- 대형 컴퓨터(메인프레임)
	- 큰 조직의 전산화를 위해 설계
	- 대기업, 은행, 증권거래소, 연구소등에서 사용하는 주전산기
- 슈퍼컴퓨터
	- 속도 빠르고 용량이 커 많은 계산을 요구하는데 사용

- 사용 기능(형태)에 따른 분류 
- 중앙집중식 전산시스템
	- 많은 사람들이 원격 단말기로 중앙컴퓨터에 접속(on-line)한 상태
- 독립형 컴퓨터
	- 혼자 독자적으로 계산할 능력이 있는 컴퓨터(집에 있는 PC)
	- 시뮬레이션 하는 컴퓨터
- 분산 컴퓨팅 혹은 분산처리시스템
	- 작업을 여러개로 나눠 여러 대 컴퓨터가 작업하여 나중에 합침

- 클라우드 서비스 
	- 클라우드 컴퓨팅을 가르킴
	- AWS, Google Cloud
- 호스팅 서비스 
	- 물리적인 실제 서버를 구축하여 서비스를 함(서버 사용)
	- 규모에 따른 유연성 부족, 고정식임(정해졍 있음)
	- 웹 호스팅
		- 웹 사이트 구축 -> 외부 컴퓨터 자원 이용 -> 웹 프로그램 서비스 활용 -> 서버 이용(회사 서버 일정기간 이용)
- 클라우딩 컴퓨팅
	- 수많은 컴퓨터가 동시에 연결(특정 서버 연결, 유연성 있음, 가상 서버 만들어 이용)
	- 네트워크 기반의 서비스, 물리적으로 실존하지 않음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/475082f8-f607-4206-b341-0a1f8614eb61/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T023349Z&X-Amz-Expires=86400&X-Amz-Signature=7c123f11ff8755f0b47b7a49944c6bfb21b59c30be4a952b52dcd3b63c6a200e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 엣지 컴퓨팅은 클라우딩을 활용하지만 중간에 매개체로 엣지 플랫폼을 활용하여 쓰는 것임
- 클라우드 기술과 엣지 기술을 적절히 섞어서 사용함

- 서버와 클라이언트
- 서버
	- 파일을 공급해주는 쪽의 컴퓨터(웹 서버는 홈페이지의 내용이 담긴 컴퓨터)
- 클라이언트
	- 파일을 공급받는 쪽의 컴퓨터(웹 클라이언트는 웹 브라우저를 이용해 홈페이지를 열어보는 일반 사용자들의 컴퓨터)

## 정보의 표현
- 코드
	- 암호나 부호
	- 컴퓨터 처리형식에 맞도록 부호화된 프로그램 명령이나 데이터
- 비트
	- 2진수 체계에서 정보의 기본 단위 1과 0 표현
- 숫자코드
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/64b60f45-1084-40d1-8a48-21c93ddcc949/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T023731Z&X-Amz-Expires=86400&X-Amz-Signature=fc2e1bb55e60c53a67c60f33fe22c17788e89c706284b28e341724ae55d2bcc2&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 숫자코드는 프로그래밍 언어마다 표현이 다름

- 컴퓨터 워드
	- 하드웨어적인 관점 
		- CPU에서 한 번에 처리할 수 있는 비트 수
	- 소프트웨어적인 관점 
		- 운영체제에서 사용하는 커널의 비트 수
		- 컴파일러에서 사용하는 데이터 단위
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/083ff28c-fd28-469b-8da6-b02aefc1ce7c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T023932Z&X-Amz-Expires=86400&X-Amz-Signature=a2ba224b9638a4bb13afd68e61a7878bc58f618f687ef966ce1a8e8d785575aa&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 데이터 단위
	- 8비트 바이트까지는 공통
	- 16비트 이상은 표현이 다양
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/288dc2ad-92a3-4f13-9f91-187dd3286336/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T024029Z&X-Amz-Expires=86400&X-Amz-Signature=eaca1c64e0903cde1d2b599774a0f170bd8b027be95ed7a9b13229bbfc5f6836&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 문자 세트와 문자 인코딩
	- 문자 인코딩 또는 코드 페이지 
		- 문자 세트를 부호화한 것, 다양한 인코딩 방법 가능
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d69deaf2-3839-4f68-8ee4-bec8515a0571/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T024135Z&X-Amz-Expires=86400&X-Amz-Signature=502e86b39eaf5d4031c66a14a516bb88683c428348d138fa198decce02e46e9e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 아스키 문자 세트
	- 7비트 인코딩 사용, 아스키 문자 코드의 집합
	- 7비트 표준 아스키 문자 세트 
		- 0~31, 127(33개) -> 인쇄 불가능한 문자(enter, delete등)
		- 32~126 (95개) -> 영문 알파벳 대소문자(52), 숫자(10), 구두법 기호등의 특수문자(32), 공백(1)
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c409f395-f651-44f7-ac48-e89c883159a1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T024320Z&X-Amz-Expires=86400&X-Amz-Signature=222f415413023503b93902dc5146097b5ffc1beac7d0ac799a3afcb4e4378f3b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- ANSI 코드
	- 8비트 확장 아스키 문자 세트
	- 외국 문자나 그래픽 문자 포함

- 유니코드
	- 전 세계 언어의 문자 코드를 모두 포함하려는 국제 표준 
	- ISO/IEC 10646
	- 약 100만개의 문자 표현, 계속 추가 가능
