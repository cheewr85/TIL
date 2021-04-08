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
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/eaba682f-4ecd-451d-9020-e211b7f0728f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T234032Z&X-Amz-Expires=86400&X-Amz-Signature=d2671a7c5e2ee44da20c46286c4806b7b3d63b4b046ae76fafd5e757a8859595&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- compile은 예전방식이므로 아래와 같이 implementation으로 수정해서 사용함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b731a721-903b-438f-ad1e-97bdea64f06c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T234108Z&X-Amz-Expires=86400&X-Amz-Signature=930b973776e44f51ac214c7ce7bd5d6f2389f5fd0f933daa01df4170e0da5491&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0739b3b8-ce13-4fcf-8438-947261a294c3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210408%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210408T234121Z&X-Amz-Expires=86400&X-Amz-Signature=e402bd54b425e2985eb74b3aa20828a9b95b22498aeea9990af8323b5edbffe6&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
