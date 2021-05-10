## Operating-System Services

### Opearting System Services
- Operating System Services는 programs이 실행할 환경, 프로그램과 유저가 services하기 위한 환경을 제공해줌
- 유저에게 유용한 기능을 제공해줌
- 그 기능을 나열하면 아래와 같음

![one](/img/OS/OperatingSystem/one.png)
![two](/img/OS/OperatingSystem/two.png)
![three](/img/OS/OperatingSystem/three.png)
![four](/img/OS/OperatingSystem/four.png)

- CLI(Command Line interpreter)
	- 명령어를 통해 사용 가능함
- GUI
	- 마우스, 키보드, 모니터를 사용함
	- 아이콘을 통해서 유저가 인식하기 쉽고 파일을 자유자재로 통제할 수 있음
- Touchscreen Interfaces
	- 위의 GUI와 유사해 보이지만 터치를 통해서 할 수 있음

### System Calls
- OS가 제공하는 서비스로써 Programming interface임
- 주로 C, C++언어로 작성되어 있고 system call에 직접적인 사용보다 API를 통해서 활용함

![picture](/img/OS/OperatingSystem/five.png)
![picture](/img/OS/OperatingSystem/six.png)


- System-call interface를 통해서 system call과 연관된 숫자들이 table을 통해서 사용할 수 있음
- 이를 통해서 API를 그저 사용하고 OS가 결과 call을 알아서 이해함, 디테일하게 알 필요 없음 
- 주로 libraries, compilers, interpreters, loaders등 run-time environment가 관리함

![picture](/img/OS/OperatingSystem/seven.png)

- 더 많은 system call을 보내기 위해서 아래와 같은 방식으로 parameter passing을 활용함

![picture](/img/OS/OperatingSystem/eight.png)
![picture](/img/OS/OperatingSystem/nine.png)

- OS에서 제공하는 System calls에 대한 다양한 종류가 있음

![picture](/img/OS/OperatingSystem/ten.png)
![picture](/img/OS/OperatingSystem/eleven.png)
![picture](/img/OS/OperatingSystem/twelve.png)
![picture](/img/OS/OperatingSystem/thirteen.png)

- 아래와 같이 다양한 예시가 존재함

![picture](/img/OS/OperatingSystem/fourteen.png)
![picture](/img/OS/OperatingSystem/fifteen.png)
![picture](/img/OS/OperatingSystem/sixteen.png)
![picture](/img/OS/OperatingSystem/seventeen.png)

### System Services
- program을 실행하고 개발하는데 편리한 환경을 제공하기 위해서 System services(utilities)를 활용함
- 아래와 같이 나눌 수 있음

![picture](/img/OS/OperatingSystem/eighteen.png)
![picture](/img/OS/OperatingSystem/nineteen.png)
![picture](/img/OS/OperatingSystem/twenty.png)

- Linkers 와 Loaders를 통해서 프로그램에 대해서 컴퓨터가 인식할 수 있도록 아래와 같이 처리를 할 수 있음

![picture](/img/OS/OperatingSystem/twentyone.png)
![picture](/img/OS/OperatingSystem/twentytwo.png)

### Operating System Structure
- 여기서 알아야 할 것은 OS는 서로 다른 고유한 System call이 존재하기 때문에 서로 다른 OS에서 같은 app을 실행시킬 수 없음 
- 대신 Interpreted language Python, Ruby와 VM을 포함한 language는 다른 OS에서도 동일하게 사용할 수 있음
- OS는 아래와 같이 디자인하고 적용하기 때문임

![picture](/img/OS/OperatingSystem/twentythree.png)
![picture](/img/OS/OperatingSystem/twentyfour.png)

