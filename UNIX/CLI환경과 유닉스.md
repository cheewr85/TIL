## CLI 환경과 유닉스

### CLI 환경

- 운영체제 → 기기에서 프로그램이 실행될 수 있도록 도와주는 역할
- 개발을 본격적으로 시작시 주요 쓰는 운영체제 외에 다른것도 사용함
- command 검은 화면에서 많이 쓰는 것(cmd 화면), command를 알아야 우분투, 리눅스 등의 운영체제를 활용할 수 있음
- UNIX가 모두 뿌리로 시작함
- 20~30개의 command를 활용함


### UNIX, 유사 UNIX
- 초기 UNIX는 C를 기반으로 해서 만듬
- 여기서 변형을 해서 다양하게 활용가능했음 → POSIX
- 유닉스를 하지 않고 UNIX를 그대로 쓴 것 → GNU(GNU is Not Unix)
- Kernel → 운영체제의 핵심 부분
- GNU + Linux Kernel → GNU/Linux → Linux라고 부름
- 이러한 Linux를 수정하고 보완하여 배포한 것들이 Chorme OS, RedHat등이 있음
- 이렇게 나온 OS들 모두 Unix를 뿌리로 다 활용이 가능함

### 컴퓨터 사용방식
- 키보드 마우스 활용 → GUI
- 키보드로 커맨드를 입력해서 활용 → CLI(Command Line Interface)
- CLI 장점을 부각시킬때 활용을 주로 함, 더 빠르게 실행시키고 사용법이 명확함

### CLI 환경
- command를 입력해서 활용하는 것
- clear → 화면을 깔끔하게 해주는 커맨드
- date → 오늘 날짜가 나옴
- cal → 이번달 달력이 나옴

![one](/img/UNIX/CLI환경/one.png)

### 커맨드 조정
- 커맨드를 내가 원하는대로 쓰기 위해서 인자와 옵션을 활용해서 쓸 수 있음
- 아래와 같이 쓸 수 있음
- 인자에 따라 다르게 작용함, 인자를 여러개 줄 수 있음
- 옵션을 통해서 해당 command에 지시를 할 수 있음
- 정해진 방식에 맞춰서 사용해야함

![two](/img/UNIX/CLI환경/two.png)
![three](/img/UNIX/CLI환경/three.png)

- 여기서 옵션을 사용할 때 아래와 같이 인자도 함께 쓸 수 있음, 여기서 이것은 옵션의 값(value) 혹은 옵션의 인자(argument)라고 함

![four](/img/UNIX/CLI환경/four.png)

- 이런식으로 옵션의 사용에 있어서 필요로 한 인자를 써야하는 경우도 있음
- 커맨드의 사용법을 모를 경우 공식 메뉴얼을 참고하면 좋음(man 커맨드 활용)