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
![one](/img/ComputerStructure/Instruction/one.png)


- CPU 제어장치의 중요한 역할
	- 명령어를 인출하여 해독하고 실행하는 일
![two](/img/ComputerStructure/Instruction/two.png)
![three](/img/ComputerStructure/Instruction/three.png)

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
![four](/img/ComputerStructure/Instruction/four.png)


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
![five](/img/ComputerStructure/Instruction/five.png)
![six](/img/ComputerStructure/Instruction/six.png)


## 병렬계산
- 병렬계산(parallelism) 혹은 parallel computing
	- 컴퓨터의 병렬처리 작업에 대한 보다 전문적인 용어
	- 병렬처리 작업을 수행하는 방법이나 구조
	- 동시에 많은 계산이 수행되는 계산 형태
		- 큰 문제는 작게 쪼개어 작은 문제들로 만들어 동시에 풀 수도 있다는 논리에서 출발
		- 병렬계산은 처음에 고성능 컴퓨터에 시작되었으나, 멀티코어 프로세스가 발달하면서 광범위하게 사용됨
		- 작업 병렬계산외는 싱글코어 프로세스도 가능\
![seven](/img/ComputerStructure/Instruction/seven.png)
![eight](/img/ComputerStructure/Instruction/eight.png)
![nine](/img/ComputerStructure/Instruction/nine.png)


## 파이프라인 구조
- 명령어 파이프라인 구조
	- 하나의 명령어 사이클을 여러 단계로 나누고 각 단계에서 동시에 다른 명령어를 처리하도록 CPU 설계
		- 이런 작업을 파이프라이닝
	- 파이프라인의 깊이는 총 단계 수
		- 각 단계는 독립적인 모듈로 구성되어 서로 다른 명령어를 다른 단계에서 동시에 처리하도록 설계
- 2단계 파이프라인 구조
![ten](/img/ComputerStructure/Instruction/ten.png)
![eleven](/img/ComputerStructure/Instruction/eleven.png)
![twelve](/img/ComputerStructure/Instruction/twelve.png)


- 4단계 파이프라인 구조
![thirteen](/img/ComputerStructure/Instruction/thirteen.png)
![fourteen](/img/ComputerStructure/Instruction/fourteen.png)


- 파이프라인의 속도상승
![fifteen](/img/ComputerStructure/Instruction/fifteen.png)


- 슈퍼 파이프라인 구조
	- 기존 파이프라인의 단계수는 유지하면서 각 단계 내에서 처리속도를 몇 배로 높여주는 CPU 설계 기술
		- 단계 내부에서 더 작은 단계들로 세분화시키고 클럭속도를 높여 빠르게 처리
	- 슈퍼 파이프라인 차수 sp를 정의
		- 파이프라인 구조의 한 단계 내에서 처리 속도를 몇 배로 높이는지 나타내는 비율
![sixteen](/img/ComputerStructure/Instruction/sixteen.png)
![seventeen](/img/ComputerStructure/Instruction/seventeen.png)


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
![eighteen](/img/ComputerStructure/Instruction/eighteen.png)
![nineteen](/img/ComputerStructure/Instruction/nineteen.png)


- 슈퍼스칼라와 슈퍼 파이프라인
![twenty](/img/ComputerStructure/Instruction/twenty.png)
![twentyone](/img/ComputerStructure/Instruction/twentyone.png)


## VLIW 구조
- CISC(complex instruction set computer, 시스크)
	- 간단한 명령부터 복잡한 명령까지 종류가 다양
		- 복잡한 기계어 명령까지 고려하므로 실행단계가 많고 회로 설계 복잡, 필요 클럭 개수도 제각기 다름
- RISC(reduced instruction set computer, 리스크)
	- 명령 축약형 컴퓨터
	- 복잡한 명령을 모두 없애고 멍령어 처리구조를 단순화해 기계어 명령의 수를 최소로 줄인 CPU
		- 이론적으로 1클럭에 1명령어가 고속 처리되도록 설계
		- 가능한 하드웨어만으로 처리해 속도를 증가
		- 범용 레지스터 개수를 대폭 늘려 외부 메모리의 액세스 횟수를 최소로 줄여 실행 속도 높음
	- RISC의 장점
		- 병렬처리 프로세서 설계에 효율적
			- 하드웨어가 덜 복잡해 CPU 설계 노력과 시간 절약
		- 과거의 통념은 RISC가 고성능 CPU의 정석
			- CISC 구조에 비해 내부 캐시나 여러 개의 명령어 파이프라인과 슈퍼스칼라 구조를 구성하기에 유리
		- 프로그램 개발에도 유리
			- 운영체제, 컴파일러 제작사, 응용프로그램 제작자 모두 -> 적은 수의 명령어만 조합해 사용하므로 편리
	- RISC의 한계
		- 명령어 종류만 줄여 CPU 성능을 높이는데 한계
		- RISC가 제대로 성능을 발휘하려면 병렬처리르 고려해 명령어를 적절히 분산시켜야함
		- RISC는 상당한 하드웨어 자원을 낭비
			- 컴파일러가 번역해준 명령어를 판독해 병렬처리가 가능한 명령이 무엇인지 다시 조사하고 판단
			- 성능을 더 높이려면 하드웨어의 복잡성이 다시 증가
		- 해결책의 하나 -> VLIW처럼 명령어 구조를 개선하고 컴파일러의 정밀성과 비중을 확대
			- 컴파일러가 명령어의 병렬처리에 직접 관여
- VLIW(very long instruction word)구조
	- 여러 명령을 묶어 매우 긴 명령어 형식을 만든 구조
	- 매우 긴 명령어 워드
		- 128, 256, 512비트 혹은 그 이상까지 사용
	- 분명하게 명시한 명령어들은 동시에 병렬로 실행
		- 병렬 처리할 명령을 컴파일러에서 미리 판단
		- 동시에 실행될 수 있는 명령들을 하나로 묶어 긴 명령어 형식 내에 재배열, CPU는 별도 판정 없이 병렬처리
	- 하드웨어 설계의 복잡성을 갖지 않는 대신 정교한 컴파일러 기술 필요
		- 프로그램 자체에 의존해 어떤 명령이 동시에 실행이 가능하고 충돌을 어떻게 피할지 판단
- IA-64 명령어 구조
![twentytwo](/img/ComputerStructure/Instruction/twentytwo.png)


- IA-64구조 -> 정교한 컴파일러 기술 이용
	- 128비트 길이 명령어 번들형식 사용
		- 번들당 41비트 길이 명령어 슬롯 3개
		- 실제 프로세서들은 여러 개 명령어 번들 형식을 사용
	- 템플릿 -> 번들 내에 포함된 명령 슬롯이 실행되는 방법을 적어 놓은 표
		- 하드웨어 자원이 부족할 때는 병렬처리 않고 일부 명령만 임시로 정지할 수 있도록 지정해주는 역할
		- 5비트 0X01~1F에서 최대 32가지 실행방법
- VLIW와 파이프라인
	- VLIW 실행차수 v를 정의
		- VLIW 구조에서 하나의 명령어 번들 형식에 포함되어 동시에 병렬처리로 실행될 수 있는 명령어의 개수
		- VLIW 실행 차수 v=3, 파이프라인 단계 수 N=4
![twentythree](/img/ComputerStructure/Instruction/twentythree.png)


## 병렬컴퓨터
- 다중프로세서(multi-processor), 병렬컴퓨터 구조
	- 복수의 프로세서를 연결해 동시 처리
		- 복수의 프로세서가 복수의 프로그램을 처리하거나, 하나의 프로그램을 복수의 프로세서에 분할해 처리
	- 대규모(massively) 병렬컴퓨터, 초병렬컴퓨터
		- 수만 개 이상 프로세서를 서로 연결해 사용하는 구조
		- 최근 경향 -> 멀티코어 프로세서를 집중 연결해 설계
	- 대규모 프로세서를 갖는 컴퓨터 시스템
		- 그리드 컴퓨팅	
			- 분산된 지역에서 필요할 때 상호 연결되어 성능 발휘
		- 클러스터 컴퓨팅 
			- 한 군데 모여 공동의 작업
- 폴린의 분류법
	- 컴퓨터의 구조를 명령어와 자료의 흐름으로 분류해서 설명
		- 벙렬컴퓨터라고 할 수 있는 것 -> SIMD, MIMD
![twentyfour](/img/ComputerStructure/Instruction/twentyfour.png)

- SISD(single instruction, single data stream)
	- 단일 명령, 단일 데이터 흐름 구조
	- 하나의 처리장치나 프로세서를 갖고 단일 명령으로 단일 데이터를 순차적으로 처리
		- 이 구조는 파이프라인 기법으로 병렬처리 효과 가능
- SIMD(single instruction, multiple data stream)
	- 단일 명령, 복수 데이터 흐름 구조
	- 복수의 처리장치나 프로세서를 갖고 단일 명령으로 복수의 데이터를 처리
		- 벡터 프로세서나 그래픽처리장치가 해당
		- 각 배열은 동일 연산을 수행하나 처리 데이터는 다른, 비슷한 패턴을 갖는 멀티미디어 데이터 처리에 적합
- MISD(multiple instruction, single data stream)
	- 복수 명령, 단일 데이터 흐름 구조
	- 복수의 처리장치나 프로세서를 갖고 복수의 명령으로 단일 데이터를 처리
		- 복수의 처리장치가 명령은 다르나 자료는 같은 비실용
		- 존재하기 힘든 구조, 우주왕복선을 제어하는 컴퓨터들
- MIMD(multiple instruction, multiple data stream)
	- 복수 명령, 복수 데이터 흐름 구조
	- 복수의 처리장치나 프로세서를 갖고 복수의 명령으로 복수의 데이터를 동시에 처리
		- 명령과 데이터가 독립적으로 실행되는 다중프로세서
		- 일을 균등하게 배분해야 고효율, 분산처리시스템 등
- 벡터 프로세서(vector processor)
	- 복수의 연산장치를 병렬로 연결해 큰 규모의 행렬이나 배열 연산을 고속으로 한꺼번에 처리하는 장치
	- 배열 프로세서(array processor)라고도 함
	- 스칼라 프로세서(scalar processor)
		- 한 번의 명령으로 하나의 데이터를 처리, SISD 구조
	- SIMD 구조의 하나 -> SIMD는 명령어 하나로 대량의 데이터를 처리할 수 있는 구조나 명령어 기술
		- 데이터 속성상 비슷한 패턴을 갖게 되는 멀티미디어 데이터를 빠르게 처리하기에 적합
			- 계속 반복되는 루프를 단 하나의 명령어로 실행
			- 펜티엄 MMX 등 1990's 말 프로세서들도 이미 채택
![twentyfive](/img/ComputerStructure/Instruction/twentyfive.png)
![twentysix](/img/ComputerStructure/Instruction/twentysix.png)


- 멀티프로세서(multi-processor, 다중프로세서) 구조
	- = 병렬컴퓨터
	- 동시에 동작하는 여러 개의 프로세서를 병렬로 연결
		- 외부 기억장치나 입출력장치는 공유할 수 있지만, 내부 레지스터와 실행 장치는 독립적으로 사용해야 함
	- 다중프로세서를 구성하는 방법
		- 하나의 칩에 여러 코어를 내장한 멀티코어 프로세서 
		- 하나의 시스템보드에 여러 개의 프로세서 칩을 장착
		- 한 컴퓨터 내에 여러 개의 시스템보드를 장착
		- 여러 대의 컴퓨터를 공동의 작업을 위해 병렬로 연결
![twentyseven](/img/ComputerStructure/Instruction/twentyseven.png)


- 멀티코어(multi-core, 다중코어) 프로세서
	- 칩-레벨 다중프로세서, 병렬컴퓨터의 가장 기본형태
		- 인텔은 2000's 중반부터 대부분의 프로세서에 채택
	- 코어로 불리는 2개 이상의 독립적인 실제 CPU 내장
		- 듀얼코어(dual-core):2개, 쿼드코어(quad-core):4개, 옥타코어(octa-core):8개 등
		- 멀티프로세서, 멀티 CPU -> 물리적으로 분리됨
	- 칩 내부 코어가 동일 다이에 존재하지 않을 수 있음
		- 다이(die) -> 실리콘 소자의 반도체 표면 위에 집적회로를 만들고 회로 판을 잘라낸 것
		- 칩(chip) -> 보통 반도체 부품을 가리키나, 반도체 공정상의 다이, 인쇄회로기판의 표면실장 부품 등 지칭
	- 각 코어들은 강하게 또는 약하게 결합
		- 공유 캐시를 사용할 수도 사용하지 않을 수도
		- 코어 간 통신을 위한 공유 메모리, 명령어 인출 및 해독장치 부분은 공유 가능
		- 그래픽처리장치(GPU)등 내장 코어가 꼭 동일치 않음
	- 다중작업 설계에 유리 -> 하드웨어의 효율적 구성
		- 프로세서 간 연동에 유리
		- 칩당 소비전력은 증가하지만 분리된 칩보다 절감
	- 소프트웨어 알고리즘도 이에 맞게 설계해야
		- 각 코어가 일반적으로 같은 일을 나눔
		- OS가 각 코어에 작업량을 적절히 분산시키고
		- 응용프로그램도 멀티코어에 적합하게 새로 설계해야
- 멀티스레드 개념과 활용도
	- 파이프라인 단계 수가 많아지면
		- 각 단계 길이는 줄고, 작업은 더욱 세분화
	- 모든 스레드가 각 단계를 다 거치는 것이 아님
		- 일하지 않고 쉬는 유휴 단계가 발생
	- 하나의 실행 장치에서 두 개의 스레드를 겹치지 않게 동시에 작업할 수 있도록 설계
		- 작업이 할당되지 않은 실행 단계는 다른 스레드의 작업을 함께 끼워 넣어 동시에 작업
	- 하이퍼스레딩 -> CPU가 놀지 않게 쥐어짜려는 기술
![twentyeight](/img/ComputerStructure/Instruction/twentyeight.png)

