## Memory

## Roadmap
- [기억장치](#기억장치)
- [메모리 계층구조](#메모리-계층구조)
- [캐시메모리](#캐시메모리)
- [캐시 매핑 방식](#캐시-매핑-방식)
- [반도체 메모리](#반도체-메모리)
- [시스템버스의 대역폭](#시스템버스의-대역폭)

## 기억장치
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5b8981a4-6b5a-4221-bbcc-5dccf6b13d9b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210406%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210406T015354Z&X-Amz-Expires=86400&X-Amz-Signature=3e6a3c02a40a86a17f900300d901d02dcb328e8c8a391a055afc9324489a858e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 메모리(memory, 기억장치)의 역할
	- 프로그램 명령이나 데이터를 저장
	- 프로그램은 메모리에서 활동 중
		- 메인메모리가 클수록 동시에 많은 프로그램을 실행
- 메모리는 프로그램의 작업장
	- 메인메모리는 현재 실행중인 프로그램들을 저장
		- 메모리가 없으면 프로그램이 동작할 수 없음
	- 메모리의 각 영역은 서로 침범하지 못하도록 시스템 소프트웨어의 프로그래머가 정함
		- 프로그래밍 언어로 작성된 텍스트 문서, 데이터 등
		- 필요한 값들을 임시로 저장하는 버퍼나 스택 등
- 램 상주 프로그램(terminate and stay resident, TSR)
	- 실행 후 종료 될 때 제거되는 다른 프로그램들과 달리 메모리에 전체나 일부가 남아 항상 대기
		- 필요할 때 부르면 즉시 나타나 일을 수행
			- 램(RAM)->메인메모리로 사용되는 램 메모리 지칭
	- 운영체제의 커널과 바이러스 백신이 대표적
		- 윈도우 운영체제는 일반적으로 램 상주 프로그램을 실행시킬 필요가 없음
	- 다른 프로그램을 사용할 때 문제가 발생할 수도
		- 바이러스 예방 백신이 램 상주된 경우
			- 다른 프로그램 설치나 하드웨어 장치 사용에 방해
- 메모리를 용도에 따라 분류
	- 주기억장치(main memory, 메인메모리)
		- 혹은 시스템 메모리 -> 프로그램의 동작에 주로 사용
		- 현재 동작하는 프로그램들과 데이터를 저장
			- 전원이 들어온 상태에서 작업이 실행 중일 때 사용
		- 주로 고속의 램 모듈 같은 반도체 메모리 사용
	- 보조기억장치(auxiliary memory)
		- 혹은 2차 기억장치 -> 자료의 저장에 주로 사용
			- 전원이 종료된 후에도 프로그램과 데이터를 안전하게 저장하는 것이 주요 목적
		- 저가격, 대용량이 요구되는 각종 드라이브가 대표적
- 메모리 용량 표시
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9ba0c623-5a64-41a5-a886-c892dbe5578b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210406%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210406T020000Z&X-Amz-Expires=86400&X-Amz-Signature=91ef4e66dfaa6d367bb923e3c8d8c2a1eab598d62f2ffdff83534836ac258491&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b42247e1-5d13-484e-883f-c4fe581bfb33/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210406%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210406T020007Z&X-Amz-Expires=86400&X-Amz-Signature=19687cdc9601c4189e00533e09f3bf0e585b1a82a49505f146469a85f6c646c6&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 엔디언(edian, endianness)
	- 메모리 주소와 같은 논리적으로 1차원적인 공간에 여러 개의 연속된 자료를 배열하는 방법
	- 여러 단위로 구성된 자료를 저장할 때
		- 빅 엔디언(big-endian) -> 큰 단위를 먼저 저장
		- 리틀 엔디언(little-endian) -> 작은 단위를 먼저 저장
		- 미들 엔디언(middle 혹은 mixed endian) -> 둘을 혼합
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0faaef06-76e3-4fbd-a57f-a596b01aa6c7/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210406%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210406T020155Z&X-Amz-Expires=86400&X-Amz-Signature=b52a4776b56559c768e5b122a5ce03dba15aa10297a989f2dc31fe7acfafc39a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8704c644-7c32-4e6c-9921-38347aa4a400/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210406%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210406T020202Z&X-Amz-Expires=86400&X-Amz-Signature=510ea0a7573e4b38c608c34a06a5772c3ae6b5b1a281677b4b383a6b894d30c6&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 빅 엔디언과 리틀 엔디언 방법
	- 어느 한 쪽이 압도적으로 좋거나 나쁘지 않음
		- 인텔 프로세서는 전통적으로 리틀 엔디언 사용
		- 일반적으로 네트워크 주소는 빅 엔디언 사용
	- 빅 엔디언은 저장 순서가 사람이 숫자 쓰는 방법
		- 프로그래머가 디버깅할 때 편리
	- 리틀 엔디언은 하위 바이트 값만 필요할 때 편리
		- 0x1A2B3C4D 중 0x4D만 읽으면 편리
	- CPU나 소프트웨어에 따라 두 방식을 선택해 사용
		- 바이(bi-), 엔디언 CPU -> 펌웨어로 선택
		- 프로그램 내부에서 바이트 순서를 바꾸어 사용