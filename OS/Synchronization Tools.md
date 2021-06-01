## Synchronization Tools

### Background
- processes는 동시에 실행되므로 언제든지 interrupt가 발생하여 부분적으로 실행을 완성함
- 공유된 데이터에 대해서 동시에 실행하는 것은 데이터의 일관성을 잃어버릴 수 있음
- 데이터의 일관성을 유지하기 위해서 cooperating된 processes들의 순서가 정렬된 실행을 보장하는 매커니즘이 필요함

### Race Condition
- 동일한 processes에서 child process를 만든다고 했을 때 인터럽트가 중간에 발생하여서 같은 pid를 생성하는데 똑같이 동일한게 2개가 생겨버리는 문제가 발생할 수 있음

![picture](/img/OS/Synchronization/one.png)

- 여기서 P0, P1에서 next_available_pid에 대해서 똑같은 pid로 접근해서 할당하는 것을 막기위한 매커니즘이 필요함

- Critical Section Problem
	- 이러한 문제의 해결법 중 하나
	- 각각의 process들이 critical section이 존재함, 여기서 critical section problem은 각각의 process가 critical section에 들어가기 윟서 entry section에서 허가를 받아야하고 그 이후 들어가면 exit section과 reminder section으로 처리가 됨
	- 즉 critical section에서는 다른것이 올 수 없고 한 번에 하나씩만 올 수 있게 처리를 함

![picture](/img/OS/Synchronization/two.png)
![picture](/img/OS/Synchronization/three.png)

- Interrupt-based Solution
	- Entry section에서 interrupt를 정지시켜 버린뒤 Critical section 진입후 일처리를 한 후 Exit section에서 다시 interrupt를 살려내는 방식
	- multi core CPU의 경우 이렇게 처리하게 되버리면 Message passing delay가 생기고 System clock의 경우 interrupt에 의해 관리되는데 막아버리면 문제가 발생함

- Peterson's Solution
	- Two process solution이고 load와 store라는 기계어 명령은 interrupted 될 수가 없다고 가정함
	- 2개의 process는 int turn과 boolean flag[2]를 공유함
	- turn 변수는 critical section에 들어갈 turn을 가르키는 것이고 flag 배열은 critical section에 들어갈 준비된 process를 가르킴
	- flat[i] = true는 process Pi가 준비됐다는 것을 의미함
	- 위에서 살펴본 3가지 상태를 아래와 같이 충족함

![picture](/img/OS/Synchronization/four.png)

- 하지만 Peterson's Solution은 단일 스레드 환경에서는 괜찮지만 현대 쓰이는 멀티 스레드 환경에서는 일관되지 않고 예상치 못한 결과가 나올 수 있음

![picture](/img/OS/Synchronization/five.png)
![picture](/img/OS/Synchronization/six.png)

- Mutex Locks
	- Mutex(Mutual Exclusion)
	- OS 개발자가 이러한 critical section 문제를 해결하기 위해 제공하는 tools
	- mutex lock을 통해 이러한 문제를 해결 가능함
	- acquire()은 lock을 release는 lock을 해제하는 것을 의미함, 여기서 acqurie과 release는 atomic 즉 interrupt의 영향을 받지 않는 명령어야함

- 하지만 이러한 해결책은 busy waiting 즉 lock이 acquired 될때까지 status는 계속해서 체크를 하고 이 상태동안 아무것도 안하는 상태인 busy waiting이 되버림, 즉 lock은 spinlock, CPU를 낭비하는 것 차라리 sleep을 시키는 게 나은게 되버림

![picture](/img/OS/Synchronization/seven.png)

- Semaphore
	- Synchronization tool이 Mutex locks 방식보다 더 정교한 방식임, processes를 그들의 활동을 synchronize 해버림

	![picture](/img/OS/Synchronization/eight.png)

- Counting semaphore
	- 정수값으로 제한되지 않는 도메인 범위까지 범위를 정함
- Binary semaphore
	- 정수값이 0과 1사이에만 범위를 둠, mutex lock과 같음

![picture](/img/OS/Synchronization/nine.png)

