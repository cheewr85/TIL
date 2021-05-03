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
![one](/img/ComputerStructure/CentralProcessingUnit/one.png)

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
![two](/img/ComputerStructure/CentralProcessingUnit/two.png)

- 비디오카드, 사운드카드 등 특수한 Processor들도 있음

- 마이크로컨트롤러
![three](/img/ComputerStructure/CentralProcessingUnit/three.png)

- 특정 산업용에 들어가는 간단한 CPU(공장, 가정용, 간단한 형태)
- 높은 bit를 사용하지 않음
- 일반 CPU보다 성능이 많이 낮음, 많은일을 하지 않음, 단순한 일

![four](/img/ComputerStructure/CentralProcessingUnit/four.png)

## 보조프로세서
- CPU 옆에 붙어있음
- 지금은 기술이 발전해서 다 CPU칩안에 다 들어감, 예전에는 PCB(Printed Circuit Board) 직접 연결했음 복잡함
![five](/img/ComputerStructure/CentralProcessingUnit/five.png)
![six](/img/ComputerStructure/CentralProcessingUnit/six.png)

- 부동소수점 처리장치
	- floating point(소수점이 떠다님, 고정되어 있지 않음)
	- 계산시 복잡, 그래서 별도로 존재
- DSP
	- 디지털 신호처리
	- DSProcessor
	- '+','x'등이 일반 프로세스보다 훨씬 빠름, 신호처리 매우 빠름

![seven](/img/ComputerStructure/CentralProcessingUnit/seven.png)

- 화소가 많아질수록 난이도, 3D등 작업 높아짐, 직접 계산해서 CPU에 넘김

![eight](/img/ComputerStructure/CentralProcessingUnit/eight.png)
![nine](/img/ComputerStructure/CentralProcessingUnit/nine.png)

- 비트맵 그래픽
	- bmp, 가장 사이즈큼, 원본 그 자체
	- 이웃하는 색깔이 같은 경우(비슷), 짧게 표현함
- 벡터 그래픽

![ten](/img/ComputerStructure/CentralProcessingUnit/ten.png)

- 성능이 부족할 수 있으므로 그래픽카드 추가 장착

## 레지스터
![eleven](/img/ComputerStructure/CentralProcessingUnit/eleven.png)
![twelve](/img/ComputerStructure/CentralProcessingUnit/twelve.png)
![thirteen](/img/ComputerStructure/CentralProcessingUnit/thirteen.png)

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
![fourteen](/img/ComputerStructure/CentralProcessingUnit/fourteen.png)

- ALU 연산 동작
![fifteen](/img/ComputerStructure/CentralProcessingUnit/fifteen.png)
![sixteen](/img/ComputerStructure/CentralProcessingUnit/sixteen.png)

- 상태 레지스터
![seventeen](/img/ComputerStructure/CentralProcessingUnit/seventeen.png)
![eighteen](/img/ComputerStructure/CentralProcessingUnit/eighteen.png)

- 세트 : 1로 만듬 / 인터럽트 : 이벤트 발생시 간섭

## CPU 명령어
- 명령어 세트
![nineteen](/img/ComputerStructure/CentralProcessingUnit/nineteen.png)

- 명령어 종류
![twenty](/img/ComputerStructure/CentralProcessingUnit/twenty.png)

- 명령어 형식
![twentyone](/img/ComputerStructure/CentralProcessingUnit/twentyone.png)

- ADD AC,C로 예시를 들면 ADD 부분은 연산코드필드(OP Code)에, AC,C는 오퍼랜드필드(operand)에 들어감

![twentytwo](/img/ComputerStructure/CentralProcessingUnit/twentytwo.png)

- 명령어 형식의 설계
![twentythree](/img/ComputerStructure/CentralProcessingUnit/twentythree.png)
![twentyfour](/img/ComputerStructure/CentralProcessingUnit/twentyfour.png)

- form을 직접 설계 가능, 레지스터로 지정해서 서로 나눠가질 수 있음

- 주소지정 방식
![twentyfive](/img/ComputerStructure/CentralProcessingUnit/twentyfive.png)

- OPCode나 operand로 구현시 모두 다 담을 수 없음, 좁을 수 밖에 없음 
- 더 큰 단위 데이터의 경우 처리가 필요함(Operand의 경우)
- 유효주소 
	- ex) A1 <- $100A, OPCode A1 .... , OPCode $100A / OPCode $A -> 직접사용(유효주소)
- 간접주소
	- ex) 0x100(유효주소) data 0x300 0x100 / OPCode 0x300(간접주소, 이를 통해 0x100 사용함)

- 주소지정 방식의 종류
![twnetysix](/img/ComputerStructure/CentralProcessingUnit/twnetysix.png)
![twnetyseven](/img/ComputerStructure/CentralProcessingUnit/twnetyseven.png)
![twnetyeight](/img/ComputerStructure/CentralProcessingUnit/twnetyeight.png)
![twnetynine](/img/ComputerStructure/CentralProcessingUnit/twnetynine.png)

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
![thirty](/img/ComputerStructure/CentralProcessingUnit/thirty.png)
![thirtyone](/img/ComputerStructure/CentralProcessingUnit/thirtyone.png)


- 맨 앞 비트는 부호로 사용함 기존 8비트가 2^8으로 0~255인 것이 맨 앞은 부호로 사용해서 줄어들어 -127 ~ +127을 활용함 

![thirtytwo](/img/ComputerStructure/CentralProcessingUnit/thirtytwo.png)
![thirtythree](/img/ComputerStructure/CentralProcessingUnit/thirtythree.png)


- 가산기, 곱셈기와 나눗셈기
![thirtyfour](/img/ComputerStructure/CentralProcessingUnit/thirtyfour.png)
![thirtyfive](/img/ComputerStructure/CentralProcessingUnit/thirtyfive.png)


- 실수
![thirtysix](/img/ComputerStructure/CentralProcessingUnit/thirtysix.png)
![thirtyseven](/img/ComputerStructure/CentralProcessingUnit/thirtyseven.png)


- 부동소수점
![thirtyeight](/img/ComputerStructure/CentralProcessingUnit/thirtyeight.png)
![thirtynine](/img/ComputerStructure/CentralProcessingUnit/thirtynine.png)
![fourty](/img/ComputerStructure/CentralProcessingUnit/fourty.png)


- 지수 바이어스
![fourtyone](/img/ComputerStructure/CentralProcessingUnit/fourtyone.png)
![fourtytwo](/img/ComputerStructure/CentralProcessingUnit/fourtytwo.png)


- 정규화형식
![fourtythree](/img/ComputerStructure/CentralProcessingUnit/fourtythree.png)
![fourtyfour](/img/ComputerStructure/CentralProcessingUnit/fourtyfour.png)
![fourtyfive](/img/ComputerStructure/CentralProcessingUnit/fourtyfive.png)


- 논리 및 시프트 연산
![fourtysix](/img/ComputerStructure/CentralProcessingUnit/fourtysix.png)
![fourtyseven](/img/ComputerStructure/CentralProcessingUnit/fourtyseven.png)
![fourtyeight](/img/ComputerStructure/CentralProcessingUnit/fourtyeight.png)
![fourtynine](/img/ComputerStructure/CentralProcessingUnit/fourtynine.png)
![fifty](/img/ComputerStructure/CentralProcessingUnit/fifty.png)


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
