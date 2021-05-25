## Threads and Concurrency

### Threads
- 다양한 task에 대해서 각각 thread를 별도로 두어 동시에 작업을 할 수 있게 함
- process를 여러개 만들어서 처리하는 것보다 thread를 여러개 만들어서 처리함으로써 더 효율적으로 사용 가능함

![picture](/img/OS/Threads/one.png)
![picture](/img/OS/Threads/two.png)

- Thread를 활용함으로써 작업을 별도로 처리하는데 수월함
- 같은 process에서 code, data, files를 공유하여서 사용하기 편함
- 훨씬 더 효율적이고 합리적이면서 저렴함

### Multicore Programming
- Multicore나 multiprocessor 시스템은 사용자로 하여금, 다양한 어려움을 겪게 함
- 이를 해결 하기 위해서 Multicore programming을 함
- 그 중 Parallelism은 하나 이상의 task를 동시에 실행할 수 있게 해주는 것임
- Concurrency는 하나 이상의 task를 진행할 수 있도록 도움을 주는 것임
	- single processor / core, scheduler가 concurrency를 제공해줌

![picture](/img/OS/Threads/three.png)

- Parallelism의 종류
	- Data parallelism 
		- 각각 같은 동작을 하는 다양한 코어 사이에 같은 데이터의 subset을 나눔
	- Task parallelism
		- 코어 사이의 threads를 나눔, 각각 thread는 특별한 동작을 함

![picture](/img/OS/Threads/four.png)

- Amdahl's law
	- 직렬과 병렬요소에서 core가 추가됐을 때의 performance를 확인하기 위해서 쓰는 공식

![picture](/img/OS/Threads/five.png)
![picture](/img/OS/Threads/six.png)

### User Threads and Kernel Threads
- User threads
	- user-level threads 라이브러리로 관리하는 것
	- POSIX, Windows, Java Threads 활용함
- Kernel threads
	- Kernel에 의해서 관리를 함
	- OS를 통해서 주로 구현이 됨, Windows, Linux, Mac OS X, Android 등

![picture](/img/OS/Threads/seven.png)
![picture](/img/OS/Threads/eight.png)

- Multithreading Models

- Many-to-One
	- 많은 user-level threads가 하나의 kernel thread에 맵핑되어 있음
	- 하나의 thread가 막히면 모든 thread가 막힘

![picture](/img/OS/Threads/nine.png)

- One-to-One
	- 각각의 user-level thread가 kernel thread에 맵핑되어 있음
	- user-level thread를 만들면 kernel thread도 생김
	- many-to-one보다 더 많은 concurrency를 함

![picture](/img/OS/Threads/ten.png)

- Many-to-Many
	- 많은 user-level thread가 kernel thread에 맵핑되어 있음
	- OS가 충분한 kernel threads의 수를 만듬

![picture](/img/OS/Threads/eleven.png)

- Two-level Model
	- Many-to-Many와 유사함, 단 user thread가 kernel thread에 묶여있음

![picture](/img/OS/Threads/twelve.png)

- Thread Libraries
	- thread를 만들고 관리하는 API를 제공함
	- kernel의 도움 없이(system call 없이) user space에서만 씀
	- kernel-level library는 OS(system call) 지원을 받음

- Pthreads
	- user-level 혹은 kernel-level로 제공을 함
	- API가 thread library의 행동을 specifies하고 implementation은 library 개발에 달려있음
	- UNIX OS에서 자주 씀

- JAVA Threads
	- JVM에 의해서 Java threads가 쓰임

- OS에서의 예시
- Windows Threads

![picture](/img/OS/Threads/thirteen.png)
![picture](/img/OS/Threads/fourteen.png)
![picture](/img/OS/Threads/fifteen.png)

- Linux Threads

![picture](/img/OS/Threads/sixteen.png)

