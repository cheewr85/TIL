## CPU Scheduling

### Basic Concepts
- CPU 자원을 멀티 프로그래밍으로 최대한 활용하려고 함
- CPU-I/O Burst Cycle, CPU 실행과 I/O를 기다리는 사이클로 구성되어 있음

![picture](/img/OS/CPU/one.png)

- CPU 스케줄러는 ready qeeue에 있는 프로세스들 사이에서 선택을 한 뒤 CPU core에 그 중 하나를 할당함
- 아래와 가팅 Queue는 다양한 방식으로 정렬이 되어 있고, CPU scheduling decision이 process에서 발생함

![picture](/img/OS/CPU/two.png)

- Preemptive and Nonpreemptive Scheduling
	- 위의 사진에서 1번과 4번의 상황에서 발생하는 스케줄링이 nonpreemptive한 상황임, 이 상황에서는 하나의 process가 CPU에 할당되어 있다면 I/O wait이 발생해도 그리고 중간에 개입이 일어나도 쭉 하나의 프로세스만 계속 진행을 함
	- 그런 상황이 아닌 것에서는 preemptive한 상황인데 현대 OS에서 대부분 사용하고 있음, 중간에 다른 process가 개입하면 현재 실행중인 process가 잠시 멈추고 개입된 process가 실행됨
- 스케줄링은 아래와 같은 개념이 주어져 있음

![picture](/img/OS/CPU/three.png)

### Scheduling Algorithm
- 스케줄링 알고리즘이 가장 효율이 높기 위해서는 위에서 정해진 기준의 상황에 맞게 충족해야함
- Max CPU utilization, Max throughput, Min turnaround time, Min waiting time, Min response time
- First-Come, First-Served(FCFS) Scheduling
	- 아래와 같이 먼저 들어온 일을 먼저 처리하는 로직임, 좀 더 효율적으로 분배하기 위해서 Waiting time을 적게 배치할 수 있음

![picture](/img/OS/CPU/four.png)
![picture](/img/OS/CPU/five.png)

- Shortest-Job-First(SJF) Scheduling
	- 각 process의 length를 연결지음, 여기서 process의 schedule의 lengths를 적은 시간으로 배치를 함
	- 주어진 process에서 average waiting time을 최소화시킴, 하지만 length를 알기 어려울 수도 있음

![picture](/img/OS/CPU/six.png)
![picture](/img/OS/CPU/seven.png)

- Round Robin(RR)
	- 각각의 process들이 CPU의 작은 부분의 시간을 쪼개서 가짐, 즉 시간을 공평하게 나눠서 실행시킴, 최대한 공평하게
	- 그리고 마지막에 남는 것은 모두 시간을 줌

![picture](/img/OS/CPU/eight.png)
![picture](/img/OS/CPU/nine.png)

- Priority Scheduling
	- 각각의 process의 우선순위를 설정함, 숫자가 작을 수록 우선순위가 높음
	- 여기서 생각할 문제는 우선순위가 낮은 process는 계속 실행이 안될 수 있음
	- 그래서 이를 해결하기 위해서 각각의 process의 우선순위를 시간이 지나면 우선순위를 높여줌
	- 이를 다른 알고리즘과도 섞을 수 있음

![picture](/img/OS/CPU/ten.png)
![picture](/img/OS/CPU/eleven.png)

- Multicore processors
	- 요즘 trend는 같은 칩안에 여러개의 processor core를 두는 것임
	- 이를 통해서 Multiple threads들이 core당 생김
	- 그래서 만일 memory stall을 통해서 진행 중에 잠깐 멈추는 상황에서 더 일을 할 수 있게 만듬

![picture](/img/OS/CPU/twelve.png)
![picture](/img/OS/CPU/thirteen.png)

### Real-Time CPU Scheduling
- Real-Time은 deadline을 잘 지키는 것이 중요함
- Soft real-time systems
	- 중요한 real-time tasks의 우선순위를 높게 줌, 하지만 모두 다 지켜진다고 보장할 순 없음
- Hard real-time systems
	- task들이 무조건 deadline에 맞춰서 진행되어야함
- Event latency가 존재함, event가 발생했을 때부터 처리될때까지 시간의 양만큼 지연이 있음
	- Interrupt latency, interrupt가 발생했을 때부터 interrupt가 실행될 때까지의 시간
	- Dispatch latency, CPU에서 현재 process의 schedule을 종료시키고 다른 것으로 바꿀때의 시간

![picture](/img/OS/CPU/fourteen.png)

- Priority-based Scheduling
	- real-time에서는 preemptive하고 priority-based하게 진행이 됨, soft real-time에선
	- hard real-time에서는 deadline을 반드시 충족시켜야함
	- 이때 CPU가 아래와 같이 주기를 가지게 됨

![picture](/img/OS/CPU/fifteen.png)

- Rate Monotonic Scheduling 
	- 우선순위가 해당 period의 반대로 할당됨
	- Shortest period = higher priority
	- Longer period = lower priority

![picture](/img/OS/CPU/sixteen.png)

- 하지만 그러다가 Deadlines을 아래와 같이 놓칠수도 있음

![picture](/img/OS/CPU/seventeen.png)

- Earliest Deadline First Scheduling(EDF)
	- 위에서 Deadlines을 놓치는 상황을 고려해서 이에 맞게 처리하는 스케줄링
	- 우선순위가 deadlines에 의해서 할당됨

![picture](/img/OS/CPU/eighteen.png)

- 이를 POSIX에서 아래와 같이 실제 활용을 함

![picture](/img/OS/CPU/nineteen.png)

### Operating System Example
- Linux Scheduling 

![picture](/img/OS/CPU/twenty.png)
![picture](/img/OS/CPU/twentyone.png)

- Windows Scheduling

![picture](/img/OS/CPU/twentytwo.png)
![picture](/img/OS/CPU/twentythree.png)

