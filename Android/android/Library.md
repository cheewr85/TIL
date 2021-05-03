## Library
- Framework
	- 안드로이드 스튜디오
	- 개발을 하기 위해 지켜야하는 툴
- Library(외부의 도움)
	- 개발을 하기위해 필요한 도구들이 미리 구현되어 있는 것
	- 함수나, 클래스로 구현이 되어 있음
	- 프레임워크에 없다!
	- 특징
		- 프레임워크에서 하기 힘든 것들을 쉽게 사용할 수 있도록 만들어 놨다!
		- 프레임워크에서 제공하지 않는 기능을 사용할 수 있도록 만들어 놨다!
- 외부에서 라이브러리가 어떻게 구현이 되어 있는지 다 접근하고 볼 수 있는 것을 오픈소스 라이브러리라고 함
- 어떻게 가져올지 Setup을 먼저 해야함 직접 파일을 추가할 수 있지만, Gradle이 라이브러리를 관리하므로 주로 이를 통해 활용함
- gradle에 앱단위와 프로젝트단위에서의 설정이 필요함
![one](/img/Android/android/Library/one.png)

- compile은 예전방식이므로 아래와 같이 implementation으로 수정해서 사용함
![two](/img/Android/android/Library/two.png)
![three](/img/Android/android/Library/three.png)
