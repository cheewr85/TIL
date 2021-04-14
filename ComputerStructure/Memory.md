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

## 메모리 계층구조
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6d5913fb-1ffb-4478-94fa-f9dfdaae8559/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T090403Z&X-Amz-Expires=86400&X-Amz-Signature=b78a400a6c3058747a4688a3ce3e9e3f633dad648d11387925e8ef1b5980d79c&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 액세스(access) -> 어떤 장소로 접근하는 동작(사용하는 시간)
	- 이미 저장된 내용을 읽기 위해 혹은 데이터를 새로 저장하기 위해 특정위치에 신호가 도달하는 동작
- 액세스 타임(access time, 접근시간)
	- CPU가 데이터의 저장 위치에 접근을 완료하거나 응답을 받기 시작하는 데 걸린 시간
		- 액세스 타임은 저장된 위치를 찾는데 걸린 시간, 전송속도는 실제 전송이 이루어지는 데이터 전달 속도
	- 기억장치나 입출력장치의 동작속도를 나타내는 척도
		- 액세스 타임이 빠르면 읽기와 쓰기 시간이 절약
		- 같은 장치라도 읽기, 쓰기 액세스 타임이 다를 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b56f41ca-21dc-4384-a472-31b67a7d9f01/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T090630Z&X-Amz-Expires=86400&X-Amz-Signature=b445767d68daa44ac7cbe8f84e21e1a77e27454247ab043e267362448a96267e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6e9f9d71-ab38-4d41-9a50-7f8663e14abf/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T090706Z&X-Amz-Expires=86400&X-Amz-Signature=ee671dcee00e73c756b1105d180071f34b5a9605935086f1bb8222718982a3b2&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- CPU에 가까이 있을수록 빠름, 자주 쓰일스록 속도 빨라짐, 소비전력은 5~8번이 1~4번보다 더 큼

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/fcd7413c-3201-4f2d-aaef-3b5cb1626227/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T090807Z&X-Amz-Expires=86400&X-Amz-Signature=8257ff40f04b25554f67df8cf5f01e116b9d24e35310c59446779565646889f1&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/210e2735-4580-4571-96ca-71cb600368e6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T090835Z&X-Amz-Expires=86400&X-Amz-Signature=016187b678d43583a219a4933f468c1e277779bd154afa81edfe30a94fe4982c&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 가상메모리
	- 프로그램이 실행되려면 동작에 필요한 최소한의 메모리가 작업공간으로 남아 있어야 
- 가상메모리(virtual memory, 가상기억장치)
	- 주로 하드디스크의 일부를 확장된 램으로 가정해 부족한 메인메모리의 일부로 사용하는 것
		- 논리적 공간이라 물리적으로 연속적일 필요는 없음
	- 부족한 메인메모리 크기를 외형적으로 늘리는 방법
		- 실제보다 많은 양의 메모리를 갖는 것처럼 동작
	- 운영체제가 자동으로 관리
		- 가상의 주소를 사용해 확장된 램처럼 관리
		- 사용자가 임의로 최대 크기를 설정할 수도

- 하드디스크 스와핑(swapping) 혹은 스왑(swap)
	- 메인메모리의 내용과 보조기억장치인 하드디스크의 내용을 상호 교환하는 것
	- 스왑 파일은 가상메모리를 사용할 때 실제 메모리인 램에 대한 확장으로 하드디스크에 만들어지는 파일
		- 윈도우나 유닉스기반 운영체제들이 사용하는 용어
		- 일반적인 운영체제 -> 페이지, 페이징
	- 파일 단위로 연속된 공간을 구성할 수 있어 적은 횟수의 읽기, 쓰기로 가상메모리를 관리
		- 메모리가 부족하면 오래 전 사용된 내용은 필요할 때까지 임시로 하드디스크에 스왑 파일로 보내짐(안 쓰는 것 카피해서 보냄, 당장 쓰지 않는 부분)
		- 사용자가 스왑 파일의 크기를 조절 할 수도
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1ad92941-87c8-41d0-87b0-b4e886d45beb/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T091313Z&X-Amz-Expires=86400&X-Amz-Signature=52320453fb81ac7c57508bc4fc07fd633036ddd6a75c57b5c70ab558ed51a946&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 페이지(page), 가상 페이지 
	- 가상메모리 공간을 일정한 크기로 나누어, 메인메모리와 하드디스크 사이에 한 번에 이동하는 단위
		- OS는 다량의 페이지로 구성된 가상메모리를 관리
	- 페이지 프레임(page frame)
		- 가상의 기억공간을 다룰 수 있도록 할당된 메인메모리 영역, 하드디스크의 페이지들 중 하나를 복사해 할당
		- 여러 개의 페이지 프레임들이 존재
	- 페이징(paging), 페이지 교체(replacement)
		- 메인메모리와 하드디스크 사이의 페이지 교환 동작
		- OS가 참고하려는 페이지가 메인메모리에 없으면 하드디스크에 저장해둔 페이지를 참조해 가져옴
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/12a8b013-1f49-4a69-a654-b815a2d41485/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T091538Z&X-Amz-Expires=86400&X-Amz-Signature=05451c340fba0c672732ccb168d91cedc3a709f68d795ad32b563fc789311e32&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 물리메모리(physical memory)
	- 가상메모리에 대응하는 용어로 실제 메모리
- 가상주소와 물리주소
	- 가상주소(virtual address)
		- 가상메모리를 관리하는 주소
		- 물리주소로 변환해서 사용해야 함
	- 물리주소(physical address)
		- 실제 메모리 주소
		- 오프셋(offset) 값을 이용해 가상주소의 비트 수 줄임
			- 페이지 프레임으로 사용하는 시작주소에서 지정하려는 주소까지 차이인 변위(displacement) 값 알면 계산
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a8908e46-d98c-4387-9800-03fc1f6a4c63/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T091731Z&X-Amz-Expires=86400&X-Amz-Signature=fce6b3f57cf1ed57d0d37abad9f9848868003404019f48854ea2304c16bc6a07&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/fa1f8f15-5a06-429a-8edb-d47ec274c45e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T091820Z&X-Amz-Expires=86400&X-Amz-Signature=16c11da1433130eccf548d7eabed80d08ad1b2c32374db7628e893df64b6d491&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/cfa0011b-874a-4a1f-a341-316a9f9ebcd0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T091829Z&X-Amz-Expires=86400&X-Amz-Signature=80ba00fd557f31d912c006613f0f3f5c6331302e06a551bac1b7db7455fcbe9d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/cc6373a0-a7f8-4dd9-b140-0dfcca55a111/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T091853Z&X-Amz-Expires=86400&X-Amz-Signature=dd3eeb8c9d3eb49e53a67c61d38b23062b5edae1054b81cbdb895f9bf3111121&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 스래싱(thrashing, 과다상태)
	- 전체 시스템 성능이 저하되어 작업의 진전이 아주 느리거나 아예 없는 상태
	- 가상메모리 페이징 동작이 과도하게 일어나는 상태
		- 페이지 교체가 너무 빈번하면 속도가 느린 디스크의 액세스 횟수가 늘어 처리속도가 급격히 떨어짐
	- 메모리나 기타 시스템 자원이 고갈되어 필요한 연산을 수행하기에 너무 부족한 상태
		- 운영체제는 응용프로그램들로부터 자원을 회수하는 방법 등을 통해 이런 문제를 해결하려고 노력

## 캐시메모리
- 캐시메모리(cache memory)
	- 주로 메인메모리의 액세스 타임을 줄이기 위해, CPU와 메인메모리 사이에 사용하는 빠른 속도의 메모리
	- CPU 캐시 혹은 줄여 보통 캐시라고 함
	- 프로그램이 현재 사용 중인 내용의 근방을 저장
		- 자주 액세스하는 데이터나 프로그램 명령을 반복해 검색하지 않고 즉시 사용할 수 있도록 준비(자주 쓰는데이터가 아니면 상당히 비효율적임)
	- 주로 액세스 타임이 빠른 SRAM 사용
	- CPU에 아주 가까운 곳에 위치하거나 아예 내장
		- 1990초부터는 주로 CPU 칩에 내장
- 캐시와 메모리 계층 
	- 캐시로 메모리 계층 간 속도 차이를 완충시켜 전체 기억장치의 평균 액세스 타임을 줄임
	- CPU에 가까운 순서대로 n차 캐시 혹은 레벨 n(level n, Ln)캐시라고 함
	- L3, L2, L1으로 올라갈수록 속도는 증가, 크기는 축소
	- ex)인텔의 3세대 Core i7 프로세서
		- L1,L2,L3로 내려 갈수록 4, 10, 35,40클럭이 소요(내장 캐시의 액세스 타임은 CPU 클럭 개수로 표시)
		- 용량은 32KiB, 256KiB, 8MiB로 커짐
- 아래의 그림은 메모리 계층구조의 일반 형태
	- CPU 고유 부분인 CPU 코어와 함께 L1,L2,L3등의 캐시가 계층구조를 이루며 내장
		- L3 캐시 -> 메인메모리 일부 내용을 저장
		- L2 캐시 -> L3 일부를 저장
		- L1 캐시 -> L2 일부를 저장
	- CPU는 상위계층부터 자료를 찾아 없으면 차례대로 하위계층으로 내려가면서 찾음
		- L1->L2->L3->메인메모리->하드디스크
		- 하위계층에 대한 액세스 횟수가 늘어날수록 평균 속도가 느려져 전체 기억장치의 성능은 저하(미스가 안나도록 해야함)
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/50f73bc7-e524-4e3d-89cb-8123469fd743/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T092745Z&X-Amz-Expires=86400&X-Amz-Signature=a5567538b9ff80397a103f08afe95eb61eef7b6fe9f1ed72988fb922b52465ed&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 같은 CPU 코어에서 캐시가 클수록 성능에 유리
	- 캐시의 위치에 따라 액세스 속도 성능 차이
		- CPU 코어 내부 > CPU 인코어 > CPU 칩 외부 순서
	- 같은 CPU 코어로 프로세서 성능을 개선하는 방법
		- CPU 코어 쿨럭 증가
		- 내장 캐시의 성능 개선 -> 용량과 연결 속도 개선
		- 멀티코어 구조
	- 내장 캐시의 연결 속도 개선 -> 비트 수와 클럭 올림
		- 외부 시스템버스 64비트, 내부 캐시 간 256비트
		- 칩 내부는 외부 시스템버스 쿨럭의 몇 배수 동작
- 온 다이(on-die), 온 칩(on-chip)캐시
	- 온 다이 -> 캐시가 CPU코어와 같은 반도체 회로기판 위에 있다는 뜻(같은 칩 안에 있다는 뜻)
- 멀티코어 프로세서에서 코어(core)의 개념
	- 독립적으로 명령을 실행하는데 필요한 부분
	- ALU, 레지스터, 부동소수점 처리장치(FPU), 독립적인 명령어 실행 장치, 단독으로 사용하는 L1,L2 캐시등
- 언코어(uncore) -> 내장된 장치 중 코어가 아닌 부분
	- 각 코어가 공통으로 공유해 사용할 수 있는 부분 
	- 명령어 인출과 해독장치, L3 공유 캐시와 칩 내부에 내장된 메모리 컨트롤러, 버스 컨트롤러, 그래픽처리장치(GPU)등은 코어개념에서 제외
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5194d64c-3486-4c33-a902-49a158eeef46/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T093225Z&X-Amz-Expires=86400&X-Amz-Signature=84fa2640d6164300a1494d352a8c062e6dd255ca4fb4c28825f33db4b49bc940&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 디스크 캐시
	- HDD, ODD등 디스크의 액세스 타임을 줄이기 위해 CPU와 디스크 장치 사이에 사용하는 캐시메모리
	- 운영체제에 의해 주로 메인메모리의 일부를 할당
		- 메인메모리의 상당 부분을 할당(많게는 1/3정도)
		- 디스크 캐시 늘리면 메인메모리가 줄어 가상메모리를 늘려야 하므로 적절한 비율을 OS가 자동으로 관리
	- 하드디스크에 내장된 디스크 버퍼
		- HDD를 읽고 쓸 때 임시로 저장해두는 버퍼 메모리
- 메모리의 이중독립버스(dual independent bus)
	- 메모리버스가 두 개의 독립적인 버스를 갖는 구조
		- CPU와 메인메모리 사이의 <외부 시스템버스>
		- CPU 코어와 캐시 사이의 <내부 캐시버스>
	- 전면버스(front-side bus, FSB, 프론트 사이드 버스)
		- 주로 CPU와 외부 메인메모리를 연결하는 시스템버스
		- 램 모듈 속도나 시스템버스의 클럭 등을 언급할 때
	- 후면버스(back-side bus, BSB, 백 사이드 버스)
		- 주로 CPU 내부에 내장된 캐시와 CPU 코어 사이를 연결해주는 캐시버스 
		- FSB보다 비트 수를 넓히고 클럭도 고속으로 설계
- CPU가 액세스한 내용은 일단 캐시에 복사
	- CPU가 요구할 때 신속히 재사용
		- 응용프로그램 사용시 불러들인 파일, 글꼴, 그림들
	- 캐시의 용량에 한계 
		- 한동안 사용되지 않았던 내용은 캐시에서 빠져 나감
	- 캐시 적중(hit)
		- CPU가 원하는 내용을 캐시에서 발견한 상태
		- 캐시에서 CPU로 정보를 읽어옴 
	- 캐시 실패(miss)
		- 원하는 내용이 캐시에 없는 상태
		- 메인메모리나 그 아래 계층에서 읽어옴
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d5954c07-0990-45a0-89dc-0fea473223c5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T093816Z&X-Amz-Expires=86400&X-Amz-Signature=555f2cdf080160b1b6745985f337ef166f237b983dc6d1fbf974842969ddd3fa&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 평균 액세스 타임
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4edf358c-2375-4dfb-b272-7fdefa04970b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T093907Z&X-Amz-Expires=86400&X-Amz-Signature=35f00ee054da3721e21154ff9346a051ab850f70a66de1e6e1dc2f388fc033fd&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/01688780-4047-4958-8657-5e524f10a988/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T093929Z&X-Amz-Expires=86400&X-Amz-Signature=fccd292e725efd20ff67286551e58b3ceb420ce2025e33768abf7f3b955d4d89&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- Ta= H1xT1 + (1-H1)xP1
	- P1 = H2xT2 + (1-H2)xTm

- 캐시는 전체 기억장치의 평균 액세스 타임을 줄이는 목적 -> 상위계층에 데이터가 존재할 확률을 높여야
- 캐시 설계에 고려할 사항 
	- 액세스 타임이 빠른 소자 -> 캐시와 메인메모리
	- 데이터의 지역성
		- 블록 단위로 현재 필요한 정보와 앞으로 예측되는 정보를 함께 인출
	- 캐시와 메인메모리의 데이터 일관성
		- 캐시의 내용을 변경할 때 메인메모리의 내용을 함께 바꾸어 주어야 -> 이때 걸리는 시간을 최소화
	- CPU 발열문제 : 적중률 높아지면 소비전력, 발열량도 높아짐
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/844f98a0-7d37-4165-bd99-4e519c062a9d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T094235Z&X-Amz-Expires=86400&X-Amz-Signature=1e4c48800c66d96b0e5ff41515638535f822727b9b911427bfd8491bf9f498a0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- idea -> 짧은 시간을 기준으로 보면 CPU가 자주 액세스하는 메모리 위치는 주로 한정된 지역에 집중
	- 시간적 지역성(temporal locality)
		- CPU에서 한번 참조한 프로그램이나 데이터는 조만간 다시 참조될 가능성이 높음
			- 짧은 시간 내 특정 데이터나 자원을 재사용하는 현상
	- 공간적 지역성(spatial locality)
		- 한번 참조된 데이터 주변에 인접한 데이터는 같이 참조될 가능성이 높음 -> 인접 저장된 배열 데이터
		- 대부분의 프로그램 명령어는 분기가 발생하기 전까지 기억장치에 저장된 순서대로 실행
			- 이를 순차적 지역성이라 부름
- 메인메모리와 캐시 간 데이터 일관성
	- 메인메모리와 복사본인 캐시는 데이터의 일관성이 유지 관리되고, 이때 걸리는 시간도 최소화해야
		- CPU는 본래 메인메모리를 액세스하려고 한 것
		- 캐시는 액세스 속도를 빠르게 해줄 목적
	- 정상적인 캐시는 메인메모리 자료의 일부 복사본
		- 본래는 메인메모리도 같은 내용을 가지고 있어야
	- 캐시가 갱신될 때 메인메모리도 함께 갱신되어야 둘 사이의 매핑 구조가 정상적으로 유지
		- 캐시만 갱신되고 메인메모리가 갱신되지 않으면
			- 서로 다른 내용을 가져 잘못된 결과를 초래할 수도
- 캐시 쓰기 정책(write policy)
	- 캐시의 블록이 변경되었을 때 메인메모리의 블록을 갱신(update)하는 방법과 시기를 정하는 것
- 연속기록(write-through)캐시
	- CPU가 캐시와 메인메모리 두 군데 데이터를 정상적으로 함께 갱신하는 방식
	- 속도가 빠른 캐시가 먼저 업데이트 된 후 느린 메인 메모리에 기록이 완료
		- 구조는 간단하지만 캐시가 갱신될 때, 느린 메인메모리를 매번 함께 액세스하므로 성능 저하
		- 가상메모리에 적용하면 시간이 더욱 오래 걸림
- 후기록(write-back)캐시
	- CPU가 캐시의 데이터만 우선 변경하고 메인메모리는 나중에 갱신하는 방식
		- 캐시의 자료가 교체될 때 메인메모리에 없는 내용이면 메인메모리로 복사한 후 캐시에서 비움 
	- 메인메모리로의 백업은 CPU 기계 사이클이 대기 상태로 여유가 있을 때 블록단위로 수시로 미리 백업
		- 하드웨어가 복잡하고 데이터가 갱신되기 전까지 메인메모리의 일부 내용이 일시적으로 무효
	- 요즘 프로세서들은 대개 Write-back 캐시 방법 사용
		- 느린 메인메모리의 쓰기 동작을 최대한 줄여 시간절약
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a89c425e-5676-40aa-8a1d-a29b335a2a9d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T112003Z&X-Amz-Expires=86400&X-Amz-Signature=4a4ac0e0fd686e6165c122e68a63ca95491c5bdfc51d606603649d0eb0db4b95&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6f8af033-ff3d-4101-b86c-b9db4746da03/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T112012Z&X-Amz-Expires=86400&X-Amz-Signature=1ce7511ef67230c52baca8b93874da66c8456b1945200d6e5fcdb10e225865fa&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 캐시 알고리즘(cache algorithm) 혹은 교체 정책(replacement policy)
	- 캐시의 내용 중 교체되어 나갈 자료를 결정하는 것
		- 캐시 적중에 실패했을 때 캐시에 공간이 부족하면 저장된 자료를 바꾸어 주어야 함
	- 가장 이상적인 목표는 미래에 가장 오랫동안 필요로 하지 않는 자료를 교체하는 것
		- 이것을 예측하는 것은 일반적으로 불가능 
	- 캐시의 매핑 방식도 넓은 의미로 교체 정책에 포함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1d6d3d33-812d-4025-a1da-79d756cc409a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T112240Z&X-Amz-Expires=86400&X-Amz-Signature=39aad60dde94665a1260baea1c900a6da47b93f527c13283a703663a0968b864&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a3408584-61fb-4ed8-ba8d-f3a2a6dee3bd/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T112249Z&X-Amz-Expires=86400&X-Amz-Signature=efdf475155780a235d8e6f3d4df091bda93c5ec2860118e00d18fe19da829f72&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6eb9de44-848b-43aa-b441-3a1b54aa569a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T112259Z&X-Amz-Expires=86400&X-Amz-Signature=d958c0c7407348e5ecea9a7f65d0523f168a09b1fb4d76ed5e9e93cb2c9e7506&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

## 캐시 매핑 방식
- 데이터 블록과 캐시 라인
	- 메인메모리 용량 > 캐시 용량(capacity)
		- 메인메모리는 데이터 블록(data block)으로 나누어짐
			- 다수의 데이터 블록들이 캐시를 공유해 사용
			- 메인메모리와 캐시 사이의 전송은 데이터 블록 단위
		- 데이터 블록 하나는 여러 개의 워드(word)로 구성
			- 워드 크기는 메모리 주소 하나에 할당되는 비트 수로 주로 1바이트 사용
		- 캐시메모리의 캐시 라인
			- 캐시메모리를 구성하는 행
			- 메인메모리의 데이터 블록 중 하나를 저장
			- 캐시의 데이터 교체는 캐시라인 단위
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f1b7a290-adf9-4da0-a066-74a3e26cf158/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T112545Z&X-Amz-Expires=86400&X-Amz-Signature=58534399c890e196c56f6ed65cc4000cbfd9b3888bf72d288264b0025d0be5fe&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3c02196b-4b1f-4c70-a8dc-8a72fb3caa65/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T112554Z&X-Amz-Expires=86400&X-Amz-Signature=6cda7a79f7a51f1694599f06c1d31805b871e7e2a62a913f9d95a36b5b8bcfcb&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 캐시의 매핑 방식
	- 메인메모리에 있는 다수의 데이터 블록들이 소수의 캐시 라인을 공유하는 방법
		- 메인메모리와 캐시의 자료를 대응시키는 방법 
	- CPU가 발생시킨 메인메모리 주소와 캐시 라인 자료를 1:1로 매핑
		- 완전연관(fully asscociative) 캐시 -> 메인메모리의 데이터 블록이 아무 캐시 라인에나 들어감
		- 직접매핑(direct-mapped) 캐시 -> 데이터 블록이 지정된 캐시 라인에만 들어감
		- 세트연관(set-associative) 캐시 -> 데이터 블록이 복수의 캐시 라인을 묶은 지정된 세트에만 들어감
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/86a29d5a-3410-41bc-ba0e-09d38a86df06/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T112807Z&X-Amz-Expires=86400&X-Amz-Signature=593b5e51512c224f0bd60881d9b4d42a57dc5af7537e96fef2c0e9494680ae7e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c9ad6c41-82a3-4175-a19a-ab9f80d8b6a6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T112815Z&X-Amz-Expires=86400&X-Amz-Signature=c375eaf4d701a0185c716fc4a4cb7ebc698da33d639bf342c4858b543966a1ce&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

