## Processes

### Process Concept
- Process는 프로그램이 실행되는 것을 말함, 하나의 process에서 명령어들을 병렬적으로 실행시킬 수 없음
- 아래와 같이 다양한 영역이 존재하는데 여기서 stack과 heap 영역은 어떤게 실행되느냐에 따라서 그 차지하는 비중이 유동적임

![picture](/img/OS/Processes/one.png)
![picture](/img/OS/Processes/two.png)
![picture](/img/OS/Processes/three.png)

### Process State
- Process의 상태는 아래와 같은 상태로 지속적으로 바뀌면서 Diagram에서처럼 돌아가는 구조를 가짐

![picture](/img/OS/Processes/four.png)
![picture](/img/OS/Processes/five.png)

- Process Control Block(PCB)
- 각각의 process에 대해 연관된 정보들이 있음

![picture](/img/OS/Processes/six.png)

- 그리고 이러한 process 처리에 있어서 scheduling 역시 처리함, CPU가 어떤것을 실행할지에 대해서

![picture](/img/OS/Processes/seven.png)
![picture](/img/OS/Processes/eight.png)
![picture](/img/OS/Processes/nine.png)

- 그리고 CPU상에서 PCB를 기준으로 아래와 같이 context switch가 일어날 경우, 상태를 저장하고 다시 불러오는 등의 일련의 과정이 일어남

![picture](/img/OS/Processes/ten.png)

### Process Creation
- Parent process는 child process를 만드는데 이러한 구조가 반복되면서 트리 구조를 띠게됨
- 그리고 process를 식별하는 것에 있어서는 process identifier(pid)를 통해서 식별을 함
- 아래와 같이 system call을 통해서 process가 생성되고 트리 구조를 나타냄

![picture](/img/OS/Processes/eleven.png)
![picture](/img/OS/Processes/twelve.png)

- exit system call의 경우, 완전히 끝내버리는것을 의미함
- wait의 경우에는 해당 process를 기다리고 잠재우는 것을 의미함
- 여기서 abort()는 자식 프로세스를 끝내버리는 것을 의미함

### Interprocess Communication
- Process들은 independent하거나 cooperating한 시스템임
- 여기서 cooperating한 process일 경우, 서로 통신이 필요함
- 이때 활용하는 기술이 interprocess communication(IPC임)
- IPC는 Shared memory, Message passing 2가지의 모델이 존재함

![picture](/img/OS/Processes/thirteen.png)

- 이런식으로 cooperating한 process가 된 경우 producer-consumer 관계가 됨
- 2가지 형태로 존재할 수 있음

![picture](/img/OS/Processes/fourteen.png)

- Shared Memory의 경우, 공유된 메모리 영역을 활용하여서 같이 사용을 함
- User Process에 의해서 실행됨, 여기서 Synchronize를 통해서 공유된 자원에서 작업을 미리 하고 있는 경우 건드리지 못하게 설정해둠
- IPC의 경우 공유된 자원없이 사용하는것을 의미함, 이를 위해서 communication link가 필요하고 send/receive를 통해서 메시지를 교환을 함
- communication link의 경우 2가지로 채용을 함
	- Direct Communication
		- 링크가 자동으로 생성되고, communicating processes가 정확히 한쌍으로 링크가 이어져 있음
		- 오직 하나의 link만 존재함, unidirectional 할 수도 있으나, 주로 bi-directional
	- Indirect Communication
		- mailbox를 통해서 메시지를 주고 받음
		- mailbox는 고유한 id가 있고 process는 이 공유된 mailbox만을 가지고 communication을 함

![picture](/img/OS/Processes/fifteen.png)
![picture](/img/OS/Processes/sixteen.png)

- Synchronization
	- message passing은 blocking 혹은 non-blocking 둘 중 하나임

![picture](/img/OS/Processes/seventeen.png)

- 이러한 IPC 기술은 운영체제에서 다양하게 활용됨
- 먼저 POSIX에서 shared memory를 생성한뒤 segement를 활용하여 object의 사이즈를 정한뒤 shared memory 기법을 활용하여 IPC 기술을 활용함

![picture](/img/OS/Processes/eighteen.png)

- Mach에서는 message based로 소통을 함, system call 역시 messages임
- 각각의 task를 Kernel과 Notify로 생성되어 가짐, 그러면 IPC에서 메시지를 통한 통신을 함

![picture](/img/OS/Processes/nineteen.png)

- Window의 경우 Message-passing을 advanced local procedure call을 통해서 함
- 아래와 같은 로직으로 조금은 다르게 돌아감

![picture](/img/OS/Processes/twenty.png)
![picture](/img/OS/Processes/twentyone.png)

- Pipes
	- 두 개의 process가 도관처럼 통신하는 것을 말함
	- 단방향인지, 양방향인지, half만 하는지 full-duplex를 하는지
	- 어떠한 관계를 형성하고 있는지, network를 사용하는지 등의 문제를 다룸
- Ordinary pipes
	- 외부에서 형성된 process는 접근할 수 없음, 일반적으로 parent-child관계를 가짐
- Named pipes
	- parent-child 관계 없이 접근할 수 있음

![picture](/img/OS/Processes/twentytwo.png)
![picture](/img/OS/Processes/twentythree.png)

- Client-Server Systems에서는 Socket과 Remote Procedure Calls를 함
- Socket의 경우 endpoint communication을 위해서 정의되어 있음
- IP Address와 port를 연결시키는 역할을 함

![picture](/img/OS/Processes/twentyfour.png)

- Remote Procedure Calls에서는 networked system에서의 processes사이의 procedure calls을 abstract해 줌

![picture](/img/OS/Processes/twentyfive.png)
![picture](/img/OS/Processes/twentysix.png)

