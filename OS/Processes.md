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

