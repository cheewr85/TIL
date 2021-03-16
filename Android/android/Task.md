## Task
- Task를 Activity로 본다면
- Stack 
	- 아래에서 위로 쌓임
	- Task가 쌓임
ex)                                         A
A  -----> B -----> C -----> B -----> A ---> B
     1    A   2    B   3    A   4    B   5
                   A                 A
- 1 -> A에서 B를 켬
- 2 -> B에서 C를 켬
- 3 -> C를 끔
- 4 -> 다시 A를 켬(다중허용)
- 5 -> 아래있던 A가 올라옴(다중허용 x)

- 켜지는 방법을 자체 속성으로 가지고 있는 경우
	- launchMode
		- Manifest에 Activity 설정
- 켜지는 방법을 지시하는 경우
	- IntentFlag
		- IntentFlag에 넣어줄 수 있음

- LaunchMode       다중허용
- standard            O
- singleTop         조건부 -> 열려고 하는 Activity가 현재 Activity면 onNewIntent 호출함(새로 만들지 않음), A/B에서 A를 열면 A를 생성하지 않고 B/A가 됨
-------------------------------------
- singleTask          X
- singleInstance      X

- IntentFlag
- FLAG_ACTIVITY_NEW_TASK
- FLAG_ACTIVITY_SINGLE_TOP
- FLAG_ACTIVITY_CLEAR_TOP 등등

- Activity는 스택으로 관리됨, launchMode, IntentFlage로 Stack을 사용자 마음대로 관리할 수 있음
- launchMode, IntentFlag는 특수한 케이스나 개발에 있어서 수정이 필요하지 않다면 건드리지 않는 편이 좋음