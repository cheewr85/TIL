## CSS3 고급
- 배치 
	- CSS3로 HTML 태그가 출력되는 위치 지정
		- HTML 태그는 웹 페이지에 작성된 순서와 달리 배치 가능
	- 배치 기능의 CSS3 프로퍼티들
		- display
		- position
		- left, right, top, bottom
		- float
		- z-index
		- visibility
		- overflow
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3ab051a6-41bb-4551-bfa5-a10da9b47d7f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210416%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210416T013222Z&X-Amz-Expires=86400&X-Amz-Signature=237239a1ecbc942d4ba27682c87c1f0791aaace864b43389f3bc93aa43746ddf&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/bdcb67c0-9c8a-490d-bf8c-0899e99cdfa3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210416%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210416T013345Z&X-Amz-Expires=86400&X-Amz-Signature=e7ed07146ece36cf691251601d54466b2a184a612b079a20a3ede9e4c1c3c043&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 박스의 배치 : position
	- normal flow
		- 웹 페이지에 나타난 순서대로 HTML 태그 배치
		- position 프로퍼티를 이용하여 normal flow 무시 가능
	- position 프로퍼티를 이용한 배치 방법
		- 정적 배치 - position : static(디폴트)
		- 상대 배치 - position : relative
		- 절대 배치 - position : absolute
		- 고정 배치 - position : fixed
		- 유동 배치 - float : left 혹은 flaot : right
	- position 프로퍼티를 사용할 때, 태그의 위치와 크기
		- top, bottom, left, right, width, height 프로퍼티로 지정
			- 이들 프로퍼티는 배치 방법에 따라 다르게 사용됨

- CSS3로 리스트 꾸미기
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b5fbefbe-fa40-44cb-a300-8a6f134e81de/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210416%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210416T013817Z&X-Amz-Expires=86400&X-Amz-Signature=856a678e9d2d4b4ae2448f5f6ed09f5008cb24fbd9fde684f9f9625788ba696d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- CSS3로 표 꾸미기
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/195dcc01-3949-47dc-ba50-798930abb19b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210416%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210416T014120Z&X-Amz-Expires=86400&X-Amz-Signature=d5c84a85c25558273f0a12d3a596eb70998217bec4c95ae2be3b84c9733bf348&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 스타일로 폼 꾸미기
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/51b7afef-c96c-4849-9bf4-aa4431122311/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210416%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210416T014226Z&X-Amz-Expires=86400&X-Amz-Signature=6ba08a352e543622ba752021eccc9087e5bd3df3d060392e24e764a209cd258d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- CSS3 스타일로 태그에 동적 변화 만들기
	- CSS3로만 HTML 태그 모양의 동적 변화 가능
		- 자바스크립트로 구현하던 것을 CSS3로 작성 가능
		- 3가지 기법 지원
			- 애니메이션(animation)
			- 전환(transition)
			- 변환(transform)
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b37cfde6-de7a-47bc-8020-8ad7cb4c83d8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210416%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210416T014448Z&X-Amz-Expires=86400&X-Amz-Signature=89fe6be643214dd57f3d1ce12d5fa905f49658e4e748be21cf5a403459518e23&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e38b460a-7760-4cd4-a3c5-a7761ed1a7da/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210416%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210416T014518Z&X-Amz-Expires=86400&X-Amz-Signature=15565eae0340b9e8fd51f93470dfed2a7241e8a78122d1bb5a94f84d0c8e89a4&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/bd0950b6-8d3f-48b1-b5d6-84e51ed2662e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210416%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210416T014553Z&X-Amz-Expires=86400&X-Amz-Signature=e4fcb6fd14a5ba27e040e7962094e5ece628aabfc016f2a255dff11c56ca17c5&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/132c7f62-3cb3-477e-9079-5c73ed7eb186/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210416%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210416T014600Z&X-Amz-Expires=86400&X-Amz-Signature=91b821ac0178810ba687ae213ab4446e89d451795f992cd25f4bb1990895b916&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

