## Instruction

## Roadmap
- [CPU 명령어 사이클](#CPU-명령어-사이클)
- [병렬계산](#병렬계산)
- [파이프라인 구조](#파이프라인-구조)
- [슈퍼스칼라 구조](#슈퍼스칼라-구조)
- [VLIW 구조](#VLIW-구조)
- [병렬컴퓨터](#병렬컴퓨터)

## CPU 명령어 사이클
- CPU의 명령어 사이클(instruction cycle)
	- 프로그램에서 주어진 명령어를 실행하기 위해 반복적으로 수행해야 하는 일련의 연속적인 동작
	- 명령 또는 명령어(instruction)
		- CPU가 동작을 수행하는데 필요한 설명이나 지시
- CPU 명령어 사이클의 기본 구조
	- 명령어 인출(instruction fetch)사이클
		- CPU가 메모리에서 명령어를 읽어오는 단계
	- 명령어 실행(instruction execution)사이클
		- CPU가 명령을 수행하는 단계
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8dcef3cc-1839-4595-9f90-4303947b4851/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T142000Z&X-Amz-Expires=86400&X-Amz-Signature=9e31bc2fc25da5fc5454d5c8aa751e22b6fc5b9cb794e83e03900960ceb75071&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- CPU 제어장치의 중요한 역할
	- 명령어를 인출하여 해독하고 실행하는 일
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0a0d3a7c-ae34-41f1-b185-74011310a5f7/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T142055Z&X-Amz-Expires=86400&X-Amz-Signature=05feb946d6f0d4fd73dbd459d45b53a861e5973d79339607f3cc4e445161d4c4&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b74762d2-7a0a-4476-a602-f6197498a386/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T142103Z&X-Amz-Expires=86400&X-Amz-Signature=26bfc46e20e3d6e1349e7cdd79c3450dc2656689c1de0b42df93b92f0a8cc13c&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 간접 사이클(실행 사이클의 일부)
	- 오퍼랜드 필드에 포함된 간접주소로부터 실제 피연산자가 저장된 위치인 유효주소를 읽어 오는 단계

- 서브루틴 호출과 복귀
- 메모리의 스택 영역
	- 서브루틴을 호출할 때 메인 프로그램의 위치로 다시 돌아올 복귀 주소를 저장
	- 스택포인터(stack pointer,SP)
		- CPU 레지스터 중 하나, 현재 상태에서 이용 가능한 스택 영역의 최종 위치를 표시
		- 항상 스택 영역의 최상위나 최하위 주소를 가리킴
	- 스택 영역에 내용을 넣거나 꺼낼 때는 SP를 기준
		- 주로 후입선출(last-in first-out, LIFO) 방식
			- 서브루틴이 완료되면 복귀 주소는 스택 영역에 들어간 역순으로 출력됨
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/37d6e0d6-d944-4d5d-a644-e07e1d4d105f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T142517Z&X-Amz-Expires=86400&X-Amz-Signature=8c1fd31da9ce3a07be6d504a55d3ef32a14f8d6d33dc55505557a2a7bb342993&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 인터럽트
	- 프로그램의 정상 처리순서를 방해하는 서비스 요구
		- 일반 서브루틴과 달리 대부분 전혀 예상치 못한 시점에서 CPU에 서비스를 요구
	- CPU 외부장치나 프로그램 요청에 의해 발생 
		- 하드웨어 인터럽트 -> 주로 CPU 외부장치에서 발생
		- 소프트웨어 인터럽트 -> 프로그램 요청으로 발생
	- 인터럽트 요구 수용하려면 CPU가 작업을 중단하고
		- 인터럽트 서비스 루틴(ISR)=인터럽트 핸들러 프로그램을 먼저 실행
		- 인터럽트 처리 전에 복귀 주소, CPU 레지스터 상태, 메모리 참조 주소 값 등을 스택에 저장, 처리후 복원
- 다중 인터럽트
	- 인터럽트 서비스 프로그램이 진행되는 도중 또 다른 인터럽트가 발생하는 환경(다중 서브루틴의 개념과 유사)
	- 인터럽트 마스크 혹은 마스킹 방법
		- 인터럽트가 발생했을 때 특정한 것을 받아들이지 않도록 금지 플래그 설정
		- 인터럽트 불가능 설정 -> 새로운 인터럽트 서비스는 허용되지 않고 대기
		- 인터럽트 가능 상태 -> 새로운 인터럽트 요구 수용
	- 우선순위 방법
		- 현재 작업보다 순위가 낮은 인터럽트가 들어오면 대기
		- 순위가 높은 인터럽트가 들어오면 먼저 처리
- 인터럽트 사이클
	- 명령어 사이클의 일부로 인터럽트 서비스 루틴의 시작 주소를 호출햏 인터럽트 요구를 처리하는 단계
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8f8c7413-e5bb-4cda-aedf-8a3e8fa4e87b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T142959Z&X-Amz-Expires=86400&X-Amz-Signature=3b833ab060710bc0ec25f33bbed26e59f9d8223b9beae6306629fb3e7db19f9b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/21f9d93f-fa9b-4dad-82ea-4946aab01707/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T143016Z&X-Amz-Expires=86400&X-Amz-Signature=0be0f1a8ff7379c9f23f3667e640ae924822c1aeec9650f0fc66e3dcdbe447e6&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

## 병렬계산
- 병렬계산(parallelism) 혹은 parallel computing
	- 컴퓨터의 병렬처리 작업에 대한 보다 전문적인 용어
	- 병렬처리 작업을 수행하는 방법이나 구조
	- 동시에 많은 계산이 수행되는 계산 형태
		- 큰 문제는 작게 쪼개어 작은 문제들로 만들어 동시에 풀 수도 있다는 논리에서 출발
		- 병렬계산은 처음에 고성능 컴퓨터에 시작되었으나, 멀티코어 프로세스가 발달하면서 광범위하게 사용됨
		- 작업 병렬계산외는 싱글코어 프로세스도 가능\
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f1108341-55f9-4bb5-8053-2db55b8e8cc9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T143316Z&X-Amz-Expires=86400&X-Amz-Signature=d4b7ec94a3254698b6753932be69a3d1cb117b1670de708d7cd3bf99082ed5c2&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/00240216-7466-4021-b5c6-90e70f6b3c8a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T143324Z&X-Amz-Expires=86400&X-Amz-Signature=14022a26965542246da2fc59c0b2c2b383b9b21f92bcf6a718a04387e04a499d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5cbc637f-6c96-40e1-ae17-7f81c78a16cc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T143350Z&X-Amz-Expires=86400&X-Amz-Signature=6c0eab80942e6202d15d61bbfc484af45db5ba00e2c5c1bc2e9a18a18d18961a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

## 파이프라인 구조
- 명령어 파이프라인 구조
	- 하나의 명령어 사이클을 여러 단계로 나누고 각 단계에서 동시에 다른 명령어를 처리하도록 CPU 설계
		- 이런 작업을 파이프라이닝
	- 파이프라인의 깊이는 총 단계 수
		- 각 단계는 독립적인 모듈로 구성되어 서로 다른 명령어를 다른 단계에서 동시에 처리하도록 설계
- 2단계 파이프라인 구조
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/96e7d094-7463-460d-8fed-8901df732863/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T143605Z&X-Amz-Expires=86400&X-Amz-Signature=4122528cdd30d84120304fc01b5e997502cc3e19c6945796d7bc99d440a6a078&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d1be13d6-2fd2-4559-8848-df0f86232b49/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T143637Z&X-Amz-Expires=86400&X-Amz-Signature=04cfaf0e1afbe727a0e08aeb9c0f255da81527dd7bddc819353737a943fc767c&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/baa68f79-986c-427f-8377-a624c75dab37/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T143646Z&X-Amz-Expires=86400&X-Amz-Signature=efcbff51f622f9dd2a49c0620c9acf1be2e8e7dd780e69ee489a9f287bb19837&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 4단계 파이프라인 구조
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e7b769cd-0d68-42a0-b70d-74046796d084/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T143715Z&X-Amz-Expires=86400&X-Amz-Signature=3b7e935b4ef24793171aca5a261692750cb93da97e2da0e7c9100160014b03ae&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/cb1129e1-56ed-4b97-8513-ed7e2826c9cd/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T143723Z&X-Amz-Expires=86400&X-Amz-Signature=20a6cac68c7e3d3cf1196762c6a4f7e20446358a666c7473f53a336a9d03b612&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 파이프라인의 속도상승
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/cb678c17-1e10-4488-9125-a3fe6b5b4bf5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T143814Z&X-Amz-Expires=86400&X-Amz-Signature=de2187c63f46646e9ec3499a97ae7f1e81cc099aee487f3ed7785c7ec545e32f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 슈퍼 파이프라인 구조
	- 기존 파이프라인의 단계수는 유지하면서 각 단계 내에서 처리속도를 몇 배로 높여주는 CPU 설계 기술
		- 단계 내부에서 더 작은 단계들로 세분화시키고 클럭속도를 높여 빠르게 처리
	- 슈퍼 파이프라인 차수 sp를 정의
		- 파이프라인 구조의 한 단계 내에서 처리 속도를 몇 배로 높이는지 나타내는 비율
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/66fa2e9d-1ad6-4e8d-a476-f7568431a5f3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T143941Z&X-Amz-Expires=86400&X-Amz-Signature=4be85a92919bdd22ac8b863010eb74cc9ffc234a2073f86a25a4b156b1f059cf&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4b722372-df5f-417e-90fa-0bfdae19b862/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T143950Z&X-Amz-Expires=86400&X-Amz-Signature=cc9fa1c65098040b0a70dc105b7cf98920bcf2977bf83e5738b4bc29d23593e8&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 파이프라인의 제약 조건 
	- 시스템 자원의 사용에 충돌이 없어야
		- 다른 단계에서 메모리나 입출력장치등 시스템 자원을 먼저 차지해 사용하고 있으면 기다려야
	- 명령어 간에 상호 의존성이 없어야
		- 앞 명령의 실행 결과로 얻은 데이터나 주소를 사용해야 한다면 실행 순서를 지키고 기다려야
	- 모든 명령어가 같은 단계를 거쳐야 낭비가 없음
		- 모든 명령이 모든 단계를 거치는 것이 아니므로 단계가 적어도 되는 명령은 시간 낭비 
	- 각 단계의 처리시간이 동일해야
		- 한 단계 주기는 가장 긴 단계를 기준 
		- 낭비 줄이려면 가능한 각 단계별 처리 시간이 같아지도록 잘게 나눠야
	- 명령어는 순차적으로 실행되어야 
		- 인터럽트나 서브루틴으로 분기가 발생하면 파이프라인에 있던 명령어들을 버리게 되므로 처리가 지연
- 파이프라인의 성능저하를 줄이는 방법
	- 지연분기(delayed branch) 활용
		- 분기 명령 앞뒤에 위치한 다른 명령어들의 순서를 적절히 재배치해 실행 순서를 바꾸는 것
	- 분기예측(branch prediction)
		- 명령이 분기하는지 예측했다 분기하면 파이프라인에 유입된 명령들을 변화시켜 처리지연 방지
			- 정적 예측 -> 컴파일러에서 분기를 미리 예측
			- 동적 예측 -> 실행 도중 발생된 자료를 활용
		- 효율 높고 비순차적 추론이 가능한 실행엔진과 다중 분기예측, 데이터 흐름분석, 예측실행 등의 기술 필요

## 슈퍼스칼라 구조
- 슈퍼스칼라
	- 한 명령어 사이클 동안 여러 개의 명령어를 동시에 처리할 수 있도록 설계한 CPU 구조
	- 여러 개의 여분의 실행 장치들이 필요
	- 요즘 대부분의 CPU는 슈퍼스칼라 구조를 가짐
	- 슈퍼스칼라 차수 ss를 정의
		- 한 명령어 사이클 동안 동시에 처리할 수 있는 명령어 개수
	- 슈퍼스칼라 구조에 필요한 장치들 
		- 여러 개의 명령어 인출 장치
		- 실행순서에 관계없이 동시에 실행되어도 무관한 서로 독립적인 명령어들을 판단해 골라내는 장치
		- 동시에 병렬로 처리할 수 있는 여러 개의 독립적인 명령어 실행 장치들
	- 한 명령어 사이클 동안 여러 명령어를 읽어와 어떤 명령이 독립적인지 찾아 그것들을 먼저 동시에 실행
		- 병렬처리를 방해하는 단골 메뉴
			- 이전에 실행된 명령어의 결과에 종속된 명령어들은 동시에 실행되지 못하고 기다려야 하므로 속도 저하
- 슈퍼스칼라 + 파이프라인
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/adfe5718-315f-4787-8ee0-62ba713d6bbb/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T144851Z&X-Amz-Expires=86400&X-Amz-Signature=6a2587c862306eda84e99e920188bbb74654a4744fdd7f5321e6018a5f6af657&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/45bbe7f4-a7a0-4f70-a515-78b54493bdb1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T144912Z&X-Amz-Expires=86400&X-Amz-Signature=9d9ac92d28ab8d7f5048acc189bb2b503a9e3b4ae03d9f1d91a2e73f90d5b033&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 슈퍼스칼라와 슈퍼 파이프라인
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8f9b7f41-ee62-4fd2-a576-33fa8489e8cd/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T145016Z&X-Amz-Expires=86400&X-Amz-Signature=358cf11606a5639b6e36e0f269c31cddb36247efe887f2c7d5e6165dcd9aea03&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/037e41d0-5a4a-4490-ac2b-217e1758ae14/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T145025Z&X-Amz-Expires=86400&X-Amz-Signature=e11de963a309092fd2b5194d073990d3fc23da8c57ccbe436daba9ad22efe748&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
