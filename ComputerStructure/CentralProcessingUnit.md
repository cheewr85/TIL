## Central Processing Unit

## Roadmap
- [CPU 프로세서](#CPU-프로세서)
- [보조프로세서](#보조프로세서)
- [레지스터](#레지스터)
- [연산장치](#연산장치)
- [CPU 명령어](#CPU-명령어)
- [제어장치](#제어장치)

## CPU 프로세서
- CPU의 기능
	- 명령어와 데이터를 처리하는 일
	- 사용자 프로그래밍 -> 메모리 들어옴 -> 특정 명령어 CPU에 들어옴
- CPU의 기본 구성 요소
	- 연산장치, 레지스터, 제어장치로 구성
	- CPU 내부 버스로 서로 연결
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ce388a34-e7ae-4ae7-8847-8fb7dee1a2df/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T091040Z&X-Amz-Expires=86400&X-Amz-Signature=aee52199c68f17bb47be63ecdf58e12918d244d376bb6a62764967c84382257c&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- CPU의 기본 구성요소
	- 연산장치(arithmetic and logic operation unit ALU)
		- 산술 및 논리연산장치
		- 산술연산과 논리연산을 수행하는 하드웨어 부분
	- 레지스터(register)
		- 연산을 위해 다양한 용도로 사용되는 CPU 내부의 일시적인 기억장소(양 작지만, 속도 매우 빠름)
		- 명령, 주소, 데이터 등을 일시저장(+ setting 값)
	- 제어장치(control unit)
		- 명령을 해석하고 실행하기 위한 제어신호 발생
		- 연산, 읽기, 쓰기 등 동작신호와 타이밍 신호

- 마이크로프로세서
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/17fcab11-8728-4d80-8683-570b29b3ad43/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T091313Z&X-Amz-Expires=86400&X-Amz-Signature=3abde27b027d82e51b92f175adf51ed755b4ebf3d073c29727c377f5783e0efe&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 비디오카드, 사운드카드 등 특수한 Processor들도 있음

- 마이크로컨트롤러
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/fecd0d99-a92d-4932-9850-f1e97d397c43/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T091418Z&X-Amz-Expires=86400&X-Amz-Signature=b80143e01a5cb46bb581cfbdb65994319935133ecf4990a6f2bb6ee65a18b85d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 특정 산업용에 들어가는 간단한 CPU(공장, 가정용, 간단한 형태)
- 높은 bit를 사용하지 않음
- 일반 CPU보다 성능이 많이 낮음, 많은일을 하지 않음, 단순한 일

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/51edd84b-eaea-478a-8e02-facdf0942e66/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T091547Z&X-Amz-Expires=86400&X-Amz-Signature=ecf8b06bee0b8eb6b934a501626983fa70fea0fe36d066a41e60f1d25660c779&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

## 보조프로세서
- CPU 옆에 붙어있음
- 지금은 기술이 발전해서 다 CPU칩안에 다 들어감, 예전에는 PCB(Printed Circuit Board) 직접 연결했음 복잡함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e60fbed6-90f2-48d8-9f39-507cdac231cf/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T091732Z&X-Amz-Expires=86400&X-Amz-Signature=b3c62d267af55831cb9fd0d8fccf721c627b1571ecb3684b74d4ef4a4a3a9dbc&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3e349d2f-5205-4aad-b088-c8954cf8a242/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T091922Z&X-Amz-Expires=86400&X-Amz-Signature=6a9e93fddf5a3541dc1d0bcd36690f79fd6d68d354f526f0bcb03aabe0dd8fe1&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 부동소수점 처리장치
	- floating point(소수점이 떠다님, 고정되어 있지 않음)
	- 계산시 복잡, 그래서 별도로 존재
- DSP
	- 디지털 신호처리
	- DSProcessor
	- '+','x'등이 일반 프로세스보다 훨씬 빠름, 신호처리 매우 빠름

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9b4593ce-5d58-46cd-92ae-22f3e867138d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T092055Z&X-Amz-Expires=86400&X-Amz-Signature=f352d812654b2eda9a990a496927416460b8bfef57f72491c7439c29dd6b4ae8&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 화소가 많아질수록 난이도, 3D등 작업 높아짐, 직접 계산해서 CPU에 넘김

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c13d11dc-0364-4ce1-8ef4-07728391203b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T092150Z&X-Amz-Expires=86400&X-Amz-Signature=15dca01a51b1626b2355fba152adda5fe2ec3cc17559ee66b93f71abf81920c5&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6b79f807-606f-4462-988f-77f323210aa0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T092246Z&X-Amz-Expires=86400&X-Amz-Signature=5e6c2504c44ad0b3cba0cb63ae41ece17646f754b03b8655c03abd4eb14d2997&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 비트맵 그래픽
	- bmp, 가장 사이즈큼, 원본 그 자체
	- 이웃하는 색깔이 같은 경우(비슷), 짧게 표현함
- 벡터 그래픽

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f5442b87-bc96-4363-9cc6-a6c7a4723adf/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T092332Z&X-Amz-Expires=86400&X-Amz-Signature=8d454399f5996ef809f53e7b99a1d0bfd8f2a52c45ccee89391953818e049db2&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 성능이 부족할 수 있으므로 그래픽카드 추가 장착

## 레지스터
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/22d1309a-e17b-4520-89c3-391d2bedcda7/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T092458Z&X-Amz-Expires=86400&X-Amz-Signature=49d827a8eaf3c05425988be174cd4849375c4efb35dadebcc95e3da5461eb367&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/609f579b-8d9e-417f-accf-36a913e6fe9d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T092541Z&X-Amz-Expires=86400&X-Amz-Signature=98685b61a57052a2c2bdaa3373015886e3928bf7470232476f3318094f283fe6&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7453dd4b-48b7-43a5-81b0-c6562e89c22b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T092550Z&X-Amz-Expires=86400&X-Amz-Signature=f50cdb2498796b65e528863ffa278849bd56c1a4f40493e5b86452dc1a22fe2b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- AC(어큐뮬레이터)
	- ex) add b,a,c -> b = a + c(명령 길음 짧아야함) -> AC 활용, add AC,C -> AC = AC + C(연산참여, 최종적으로 사용, 표현식이 짧고 간단해짐)
- PC(프로그램 카운터)
	- 다음에 인출해올 명령어의 주소를 저장
	- 다음에 실행할 주소 저장
	- 다음에 가져올 주소에 대해서 알려줄 매개체가 필요할 때 그 역할을 PC가 함
	- ex) 100 add AC, C / 101 sub AC, d -> PC => 100 -> 101
	- ex) 100 Go 200 / 101 sub AC, d -> PC => 100 -> 200
- MAR(메모리 주소 레지스터)
	- 주소를 출력하기 전에 임시로 저장
	- CPU에서 메모리에 주소를 줄 때 메모리 주소 레지스터에 둔 다음 줌(주기 전 임시로), 주 핀으로 나가기전에 저장(CPU-Memory), MAR에 저장후 핀으로 나감
- MBR(메모리 버퍼 레지스터)
	- MAR과 유사한 로직, 단 data인 케이스임
- IR(명령 레지스터)
	- PC register,명령어 주소를 가져옴 -> 명령어를 담음(IR)
- 기타 범용 레지스터
	- 다양한 용도로 쓰임

## 연산장치
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c27f1655-dfb5-43bf-972b-6c27aac97ef9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T093310Z&X-Amz-Expires=86400&X-Amz-Signature=91f8de7a447c05d159dda3fde48ac09ac6fec98c260c6b6b4f8c7bf6099094ce&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- ALU 연산 동작
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d2fd2d96-175b-4626-a5ba-3599290d25f5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T093408Z&X-Amz-Expires=86400&X-Amz-Signature=c7db3c3b79098dbc43e75bec38ef760fb3a37f119435c33650cab4ef83a2414d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/980fecb6-7429-4c6f-8c8e-ef4fe21b38bc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T093417Z&X-Amz-Expires=86400&X-Amz-Signature=d59de67588d60019764b3d5c3d604e7215fdfe90b11204f050d18654961a6de5&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 상태 레지스터
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e92de386-1b27-437d-9c4a-5341e4922bf7/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T093521Z&X-Amz-Expires=86400&X-Amz-Signature=b88b8d5a4e34f0fefd8b34fe56241a238e8b1f1cf6a1c8a0fa1157aa2e0b009d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/655abae3-c40a-45a8-a33b-a2f55e2b94db/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T093530Z&X-Amz-Expires=86400&X-Amz-Signature=334f3ca75ac1c363b3bae795cebedc720ca415f36514fa717ac64514a1cf18c0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 세트 : 1로 만듬 / 인터럽트 : 이벤트 발생시 간섭

## CPU 명령어
- 명령어 세트
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ba549c32-c0bf-4dd5-9d64-da9800d3d011/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T093721Z&X-Amz-Expires=86400&X-Amz-Signature=849976d05c5c9ed4beb6158258f03d596bd54f52b84ad4fa3d244fe89dae6999&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 명령어 종류
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d5e74450-5618-426b-ad97-0ce52772a479/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T093751Z&X-Amz-Expires=86400&X-Amz-Signature=7c17264624fdc0ad7283461f89a28249b03d2fdd0c7f761c125cdbbf03328ec4&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 명령어 형식
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4fd44fac-7034-4df0-b85d-18b163d86e17/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T093827Z&X-Amz-Expires=86400&X-Amz-Signature=62b7bcd1031c38a6290b2c713d8051b9cb5ec064357a7155c137a99dda28c096&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- ADD AC,C로 예시를 들면 ADD 부분은 연산코드필드(OP Code)에, AC,C는 오퍼랜드필드(operand)에 들어감

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6542de55-644d-4f51-b3c1-36647675633a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T093957Z&X-Amz-Expires=86400&X-Amz-Signature=c57f707ddfdf1ef63d3ea564a907338cfdd36ba1f2b1a3bb970a66702cc13531&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 명령어 형식의 설계
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c3969d1f-65e8-4bdd-84a6-6b9e2b457bc9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T094103Z&X-Amz-Expires=86400&X-Amz-Signature=9dc105c4d24901aaa4512b30e9b018154fb9fc8955fc85db5ccd261da4875890&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/61583fb5-0ecb-47a9-850e-0f007f31a91e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T094131Z&X-Amz-Expires=86400&X-Amz-Signature=792d1608c0036422505cde2f5d22d2149fea3e373426decd028033d4f358cf61&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- form을 직접 설계 가능, 레지스터로 지정해서 서로 나눠가질 수 있음

- 주소지정 방식
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/155b2078-89d2-47f3-91d2-8771117c705e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T094319Z&X-Amz-Expires=86400&X-Amz-Signature=0151b5241cbb11decafe915ee5083c3f6b546f138cb48e5d35eeb5fdc718c39a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- OPCode나 operand로 구현시 모두 다 담을 수 없음, 좁을 수 밖에 없음 
- 더 큰 단위 데이터의 경우 처리가 필요함(Operand의 경우)
- 유효주소 
	- ex) A1 <- $100A, OPCode A1 .... , OPCode $100A / OPCode $A -> 직접사용(유효주소)
- 간접주소
	- ex) 0x100(유효주소) data 0x300 0x100 / OPCode 0x300(간접주소, 이를 통해 0x100 사용함)

- 주소지정 방식의 종류
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3fce0b9d-d81a-4e51-bc36-5623b8fabc0e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T094654Z&X-Amz-Expires=86400&X-Amz-Signature=1efeaf8259a5f87e98443ddb8b265422f7004827fb8e4db720aa5e4ad7fdac3a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/002acc65-aa97-4b9f-affb-287f339755fc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T094703Z&X-Amz-Expires=86400&X-Amz-Signature=098af102daa37506942bfd7dd30ae446e3fdd259af3b5ac79b2195da50c8d7f4&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9a936b95-deaa-40df-b53d-595439589c6f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T094724Z&X-Amz-Expires=86400&X-Amz-Signature=de8d651083df67c2e98a2ee613d3e49707fb640b6c52933cc3dfe6092689a72f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4c0e5a58-07c8-4eb2-aa57-001652ac56a8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T094740Z&X-Amz-Expires=86400&X-Amz-Signature=dc71f18e10018a97e04e38cebd6873b2ddc0c4f8d1f3a7f8ffdbf170597b09d0&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 암시적 주소지정 방식
	- 사용시 알아서 씀, 위의 내용처럼 INC 하나만 쓰면 알아서 AC <- AC+1이 처리됨
- 즉치 주소지정 방식
	- 실제계산숫자 바로 씀, 즉시 사용할 수 있는 데이터 수치
- 직접 주소지정 방식
	- 유효주소 사용
- 간접 주소지정 방식
	- 간접주소 사용
- 레지스터 주소지정 방식
	- 실제 피연산자 사용
- 레지스터 간접 주소지정 방식
	- 레지스터에 유효주소 저장
- 상대 주소지정 방식
	- PC에 저장된 주소값과 변위값 d를 더해 유효주소 계산
- 인덱스 주소지정 방식
	- PC 사용하는 대신 인덱스 레지스터 IX를 별도로 사용하여 계산, PC를 직접 건드리면 문제가 될 수 있으므로, 배열과 유사

- 정수의 산술연산
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/32fc613a-ee57-4153-9002-bb696d026cef/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T095208Z&X-Amz-Expires=86400&X-Amz-Signature=67bd7150b97e9c9da6e4d2bcf764208e691f3318759f5f6d5a1eda5f983ee94a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/130e6050-7654-4019-9fd2-4827a3d9584e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T095320Z&X-Amz-Expires=86400&X-Amz-Signature=ba870d7abb18aacb22e97f70f76852f86c0da50709006bea2184b45b05564532&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 맨 앞 비트는 부호로 사용함 기존 8비트가 2^8으로 0~255인 것이 맨 앞은 부호로 사용해서 줄어들어 -127 ~ +127을 활용함 

<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f2aef7c6-c4db-4293-8dc5-6ea610000e27/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T095510Z&X-Amz-Expires=86400&X-Amz-Signature=3d93c413e149b1dec9efaae740557e82c1254e48fceba300b73839fc36091cad&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6e408d58-5bac-4c6a-9873-5c4ba1c17fe7/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T095518Z&X-Amz-Expires=86400&X-Amz-Signature=1559f95681e4ea0f5b1910978a88333eea4efb79e7c8487240b22ea7a3c50716&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 가산기, 곱셈기와 나눗셈기
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/419dcda9-f15f-4ac6-9329-acee51f0da56/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T095603Z&X-Amz-Expires=86400&X-Amz-Signature=e686dc591d1fd5659c50162e0875c11ae18227eed8af76964fa5af63ded9290e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f71e80b3-0a67-4cd0-aae3-8db51782becc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T095611Z&X-Amz-Expires=86400&X-Amz-Signature=7791fa3cc7b2902c4867928f9e7c4a5135f8e18cc37ff709288d33a817df202b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 실수
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7b249aad-729f-4f09-a62f-1403bfcc2d9a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T095658Z&X-Amz-Expires=86400&X-Amz-Signature=2be5a33af36addbe5e95b92539465bd3178ddb638de7da666916d60e675800a5&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8278fa1d-a1ce-444c-baaa-7d126d2bfb3c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T095712Z&X-Amz-Expires=86400&X-Amz-Signature=3abaa698055a961f2dd5b3cde954ebb350a3d50004d7eac21d0183e5b03051b4&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 부동소수점
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/55d50012-070a-4620-a585-6bc13754ec22/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T095804Z&X-Amz-Expires=86400&X-Amz-Signature=3ac40c6731483a71c77c3efee6acaf1087281c037adc8ada49deaa0c879a95b1&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/57f0e444-6987-4c27-97ec-5fcc6c174eba/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T095813Z&X-Amz-Expires=86400&X-Amz-Signature=1585431a754039cd2a497da011d23dfdb8a0e2f2091335b803173a7330a68af7&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b0891a24-a0fd-452c-959e-ac9cbcb77a0e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T095851Z&X-Amz-Expires=86400&X-Amz-Signature=7b5115435d8630a7250d988dde92f18c8079b2c63a5e1049629664594a20fb63&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 지수 바이어스
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3f66a296-1b67-4763-8870-6dfc32ec739d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T095931Z&X-Amz-Expires=86400&X-Amz-Signature=c8eb158f7e58556a967e3bca5466842ca975db1749dbb975a57472b06cea2fb9&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3dc228d9-7abb-403d-851d-ccc1612bb7ee/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T095939Z&X-Amz-Expires=86400&X-Amz-Signature=8cdd64f31b9dbe2736562c686eabde5a15c3eb59674ef7606daa0aca716fb66e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 정규화형식
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e0ea5ff8-7eb2-4d75-bab8-8faeb26af765/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T100039Z&X-Amz-Expires=86400&X-Amz-Signature=fef498482a0a7341e8fcf5149c342dd4b3e7ce52744935a696314a069c2db128&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/290c782d-49f3-4387-a4e3-25d37a3d4964/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T100051Z&X-Amz-Expires=86400&X-Amz-Signature=0a0344d174ee4877793d31256423c921772635558400277f73c809a7a373e0cb&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/96c58cad-8ea0-45c4-82f0-9f09a1363b25/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210325%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210325T100100Z&X-Amz-Expires=86400&X-Amz-Signature=0431c2dcfe2cd767cc1a7f62741fac8cd1fedb77964eb868bcc366589e193036&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 논리 및 시프트 연산
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9822d24e-d34a-48c8-9579-c63145b71f9f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T140936Z&X-Amz-Expires=86400&X-Amz-Signature=210e174ef606f31509bf4082490350f4b153eb800c79dd1069a2a77525c9bd8b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5eb373f7-18e0-419d-9e02-9491f6525bd5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T141021Z&X-Amz-Expires=86400&X-Amz-Signature=5a309c57698c735ed0772351c1f5e3d64dd846c3afcd892367fc704244aa4f39&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/419e1f1d-511b-4bd5-a9e8-b228fe62df71/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T141043Z&X-Amz-Expires=86400&X-Amz-Signature=a4b21083c0d465373b3832f5494bae8c9aabbf0bf7587e949cefce73ac92352a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0f85a568-5242-4408-b564-512ce3bad995/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T141108Z&X-Amz-Expires=86400&X-Amz-Signature=7efd94155b9f364f7d97b84f447ad3408c35c67b5e565b2ca51a26a5993f2e4a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1c385a92-75b6-4edf-95c8-89d827170eed/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T141130Z&X-Amz-Expires=86400&X-Amz-Signature=810762cbbdea46448f8a9d73db3ee5026778a6f6061ef4cb9ca815fc146bef42&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

## 제어장치
- 제어장치의 역할
	- 메모리에서 명령어를 인출해 해독하고 명령을 실행하는데 필요한 제어신호를 발생
	- CPU 내외부에 필요한 제어신호를(때맞추어) 발생
		- CPU 내부 버스 제어신호
		- ALU와 레지스터 연산에 필요한 동작신호
		- CPU 외부 메모리나 I/O 장치에 읽기와 쓰기 신호 등 
	- 2가지 설계방식
		- 하드와이어 제어방식
		- 마이크로프로그램 제어방식
- 하드와이어(hardwired) 제어방식
	- 하드웨어만으로 마이크로연산을 수행하도록 구성
	- 실행속도는 유리하나 설계 유연성 떨어짐
		- 명령어 종류나 설계를 바꾸려면 하드웨어 부품이나 배선을 재구성해야 하므로 큰 불편
- 마이크로프로그램(microprogram) 제어방식
	- 제어메모리에 저장된 마이크로명령어를 찾아 순차적으로 실행, 대부분 이 방식을 사용
	- 유연하고 체계적인 제어장치를 구성
		- 명령어 설계가 바뀌어도 제어메모리에 저장된 프로그램만 변경
