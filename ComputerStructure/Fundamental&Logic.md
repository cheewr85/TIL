## Fundamental & Logic

## Roadmap
- [하드웨어의 구성](#하드웨어의-구성)
- [소프트웨어의 역할](#소프트웨어의-역할)
- [다중작업](#다중작업)
- [시동과정](#시동과정)
- [신호선의 동작](#신호선의-동작)

## 하드웨어의 구성
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/db63d551-9048-4b5d-aa6b-d32524de5145/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T025006Z&X-Amz-Expires=86400&X-Amz-Signature=80bf64251ac740de165bbe77d88b67273e0ef13e592dee093a85eda90520ee70&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 중앙처리장치(CPU)
	- logical, 산술계산, 프로그램제어(시작 -> 끝)
	- 프로세서라고도 함
- 기억장치(memory)
	- 프로그램 코드나 데이터 기록
	- 주기억장치(main memory, DRAM)
		- 프로그램 실행 중에 주로 사용, 반도체 메모리
	- 보조기억장치
		- USB, HardDisk, 느린속도 < memory 속도, SSD(solid-state), flash memory
		- 데이터 저장에 주로 사용, 각종 드라이브
- 입출력장치(I/O device)
	- 키보드, 통신, screen, 모니터등, interface
	- 컴퓨터와 사용자간 인터페이스
- 버스(Bus)
	- Data Address control

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/536142a1-5e2b-4e11-83a2-94ba83bfd7f9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T025401Z&X-Amz-Expires=86400&X-Amz-Signature=876988605afc6ddc9ea3a2f60d5548e1d2cab31e80e09bd35b0ceec7fa2ca5ba&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f7f90969-9b92-4ba9-8cca-9fcfd7599032/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T025819Z&X-Amz-Expires=86400&X-Amz-Signature=97d8370e654d751addf15febb9ac18213d8ea5a8ffb3c837009aff4190b039b6&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- CPU부
	- CPU와 시스템 제어를 위한 칩셋(노스브리지, 사우스브리지)부분
- 메모리부 
	- ROM
		- Read Only Memory
		- 바꿀 수 없음 , 전원을 꺼도 데이터가 유지됨
	- RAM
		- Random Access Memory
		- 바꿀 수 있음 , 전원을 끄면 사라짐
- 입출력장치 접속부(interface)
	- CPU와 입출력장치의 인터페이스 부분


<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/da75756d-de8e-48fb-bd96-209be5129d92/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T025930Z&X-Amz-Expires=86400&X-Amz-Signature=5d406e79b61a3ee49130280ad51e18c943ce489d60e46a14e04d8a0b10e619c6&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 버스의 필요성((b) 그림)
	- 자주 사용하는 신호선의 배선 수를 줄임
	- 자원 공유, 한번에 1번, 전용통신채널 없음, 부품 핀, 배선수 줄일 수 있음
- (a)의 경우 성능은 좋으나 부품이 커지고 선을 하드웨어 연결해야함
- 버스
	- 정보를 교환하기 위해 CPU와 하드웨어 요소들을 연결해주는 신호선들의 집합
	- 주소버스(address bus)
		- CPU가 외부로 내보내는 주소 신호, 단방향 전송
		- 주소버스 배선 수 -> 외부 기억장치의 최대 용량 결정
	- 데이터 버스(data bus)
		- CPU가 메모리나 I/O 장치와 데이터를 주고 받는 통로 
		- CPU가 한 번에 전송할 수 있는 비트 수, 양방향 전송
	- 제어 버스(control bus)
		- CPU 내외부의 장치를 동작시키는 제어신호(읽기와 쓰기 신호)
		- 단방향 또는 양방향 전송

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9fe4b94b-3b6e-4fbe-9218-e2f46a344550/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T030343Z&X-Amz-Expires=86400&X-Amz-Signature=8a724528349a3b156c7fa27b8c1f873798bc4ba0de9128e7dd0bf75379e1f61f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 워크스테이션과 서버도 대개 이런 구조
- 상위 기종은 CPU 성능을 높이고(쿨럭속도를 고려하여 코어를 늘림, 쿼드코어) 고속의 소자를 사용
- 메모리 주소와 I/O 주소
	- 하드웨어 측면에서 메모리와 입출력장치 구분
	- 메모리 주소 -> 주로 반도체 메모리(DRAM, SRAM)
	- I/O 주소 -> 나머지 장치들
		- HDD는 보조기억장치이나 하드웨어적으로 I/O 장치
- 메모리 컨트롤러와 I/O 컨트롤러
	- CPU를 도와 하드웨어를 제어, 대개 칩셋으로 구성 
	- 메모리 컨트롤러 -> 메모리 장치를 제어(DRAM 메모리등의 시스템버스 동기화)
	- I/O 컨트롤러 -> 입출력장치를 제어 
- 시스템버스와 I/O 버스
	- 시스템버스
		- CPU, 메인메모리, 칩셋들과 연결
		- 램 모듈을 CPU에 동기시킴(제어시간 절약)
	- I/O 버스
		- I/O 컨트롤러와 입출력장치 사이를 연결
		- 비트 수와 속도가 다양한 여러 종류의 I/O 버스 사용
- 칩셋
	- 제어칩(controller)의 모임, 여러 칩과 회로가 모임
	- CPU 프로세서와 함께 시스템 전체를 제어
	- 칩셋 내부 회로 -> CPU를 지원하는 각종 제어 장치들(버스, 메모리, I/O, 인터럽트 컨트롤러, 타이머등)
	- 메모리 컨트롤러와 I/O 컨트롤러가 기본 구성
		- 노스브리지 : 메모리 컨트롤러 포함, 고속의 장치들
		- 사우스브리지 : I/O 컨트롤러 포함, 저속의 장치들
		- 프로세서와 펌웨어 칩까지 한 구성으로 보기도 함
	- <브리지>, <허브>
		- 칩셋이 중심연결장치라는 뜻
		- MCH(memory controller hub)
		- IOH 혹은 ICH(I/O controller hub)
	- 구성 추세
		- 비디오 어댑터 인터페이스를 내장
			- 노스브리지에 포함(그래픽 전용 채널로 설계)
			- CPU에 내장, 저가 설계의 그래픽처리장치(GPU)
		- 프로세서 칩에 노스브리지 내장
			- 램 모듈, 비디오, 사우스브리지를 독립채널로 분리
				- 데이터가 몰리는 시스템버스(FSB)의 병목현상 해결
				- 램 모듈 접근속도 높여 멀티코어 프로세서 성능 향상
			- 전통적인 노스브리지의 거의 모든 기능을 CPU 내장
		- 프로세서 칩에 칩셋을 모두 내장
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/db318d9a-edeb-4813-b3f2-d85bd7157fdd/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T033340Z&X-Amz-Expires=86400&X-Amz-Signature=ae55b606f6b13685b0513ade289c899a4d038676797327c2e8a5e2f64c93367e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6e616bed-6eca-4cdc-937d-dd86c6dc587d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T033802Z&X-Amz-Expires=86400&X-Amz-Signature=8402048755023e6478d4ec5a3e47d705787577b4da86cba34d7e3a02c749fde1&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3fde3a42-f7d5-455f-a136-9f4b5d4c04d1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T033739Z&X-Amz-Expires=86400&X-Amz-Signature=f5b9aaa05699fdc1ad8585e924fd1c7d448087c03ddda84c65a201ff02fb2a85&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 메인보드(main board) = 시스템보드(system board) = 마더보드(motherboard)
	- 컴퓨터 시스템의 주기판
- 메인보드 제작규격 -> 폼팩터라고도 함
	- ATX, BTX 규격등(규격화)
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/29efd30a-6cbf-4306-bf4e-61cc952ffe28/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T034035Z&X-Amz-Expires=86400&X-Amz-Signature=641eea5e9081634385cb2e1ca3311a4710f876d27753066478249cc0c72625c8&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a5279d56-c385-4d86-ae57-47f707391852/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T034110Z&X-Amz-Expires=86400&X-Amz-Signature=33dc3cea4cf69adbe197ecb2973d4ccce6d4976b8419dc3001d9ddcdbaa3eeb2&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5ca89ad4-35be-4908-a80c-a0663c39d5de/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210311%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210311T034136Z&X-Amz-Expires=86400&X-Amz-Signature=ee6de1d92a578dc90e5165ffba27894c94d16306200097b5d8f7155d129644af&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
