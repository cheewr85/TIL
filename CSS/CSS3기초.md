## CSS3
- CSS(Cascading Style Sheet)
	- HTML 문서의 색이나 모양 등 외관을 꾸미는 언어
	- CSS로 작성된 코드를 스타일 시트(style sheet)라고 부름
	- 현재 CSS3 : CSS level 3
		- CSS1 -> CSS2 -> CSS3 -> CSS4(현재 표준화 작업중)
	- CSS3의 기능
		- 색상과 배경
		- 텍스트
		- 폰트
		- 박스모델(Box Model)
		- 비주얼 포맷 및 효과
		- 리스트
		- 테이블
		- 사용자 인터페이스
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/04602c5c-b8ec-4ae0-8a06-6d51b2585a8a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T124136Z&X-Amz-Expires=86400&X-Amz-Signature=6157bafbeb1d2e3fa6dfdb2c3d7fecc13c9b317e51f098b343a9606f5a013025&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- CSS3 스타일 시트 구성
	- 셀렉터
		- CSS3 스타일 시트를 HTML 페이지에 적용하도록 만든 이름
	- 프로퍼티
		- 스타일 속성 이름, 약 200개 정도의 프로퍼티 있음
	- 값
		- 프로퍼티의 값
	- 주석문
		- 스타일 시트 내에 붙이는 설명문으로 여러줄, 아무 위치에나 사용가능
	- 대소문자 구분 없음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/45029a17-af32-4f3d-98fd-b588295d10ba/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T124347Z&X-Amz-Expires=86400&X-Amz-Signature=7f02f8bda638fa3056cc05f183f718212e12ab283c6fda5cdaf334a431b8857d&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/cee3a3b1-759b-4e1f-9ace-b31278ead7b1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T124356Z&X-Amz-Expires=86400&X-Amz-Signature=69e9864ac6866339a613adccbb518268a7944a489c4d23953db8ed2f2740a155&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- HTML 문서에 CSS3 스타일 시트 만들기
	- style 태그에 스타일 시트 작성
	- style 속성에 스타일 시트 작성
	- 스타일 시트를 별도 파일로 작성
		- link 태그나 @import로 불러 사용
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0117493a-f311-4e46-9a1d-edd6b1abb1e4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T124511Z&X-Amz-Expires=86400&X-Amz-Signature=0ef1e80eab953a1383dcebb26f53a1db4da807f55f7ddc4f37ff9bc609d2a184&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2a8d2540-5e93-468b-88df-c5abad6d8da9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T124531Z&X-Amz-Expires=86400&X-Amz-Signature=c1b029d7f5530cf9c6de9be7681459794a7d7e5c9eba9465011f50ff2418a0ca&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/67628c96-6cb5-4ded-9a98-6caf64406d0b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T124604Z&X-Amz-Expires=86400&X-Amz-Signature=4f2f900dd00c45386be062e0b3c26ae439beeb29f413fc013c4edf8e5bd38347&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- CSS3 규칙 - 스타일 상속
	- CSS3 스타일은 부모 태그로부터 상속
	- 부모 태그(부모 요소)
		- 자신을 둘러싸는 태그
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/83ab781e-1522-4301-8216-2690fa91e228/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T124908Z&X-Amz-Expires=86400&X-Amz-Signature=998648bbc56f8e3f80bf36cda252dddce3839a98e8575dee4d55bc204c8df45b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0b4dd674-120b-4d65-a8de-637b1b60cf27/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T124922Z&X-Amz-Expires=86400&X-Amz-Signature=4b3e75e7eca8583adfd258f2686d0f5ee24ba9cbed832af97a6ebbf7fdec8656&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 스타일 합치기와 오버라이딩
	- 태그에 적용 가능한 스타일
		- 브라우저의 디퐅트 스타일
		- 스타일 시트 파일에 선언된 스타일
		- style 태그에 선언된 스타일
		- style 속성에 선언된 스타일
	- 스타일 합치기와 오버라이딩이란?
		- 태그에 적용되는 모든 스타일이 합쳐지고, 동일한 스타일은 순위가 높은 스타일이 우선 적용되는 규칙
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f9cb4270-02a9-4496-8167-d9bbf6a5b4c3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T125730Z&X-Amz-Expires=86400&X-Amz-Signature=477d6ec9ddab192e29d22e5381289375a3b371ef3881df742bd716547dc835b8&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 셀렉터
	- HTML 태그의 모양을 꾸밀 스타일 시트를 선택하는 기능
		- 여러 유형의 셀렉터
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a88ae39a-436e-4001-95f6-a93168092737/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T125827Z&X-Amz-Expires=86400&X-Amz-Signature=2e35cbc0b42a6d70e6b800e815ba50813ca3238d2690164bb01bfcac44a6588f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 태그 이름 셀렉터
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4d81df77-dec2-40d0-b3d7-6d7dff223698/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T125945Z&X-Amz-Expires=86400&X-Amz-Signature=8054eab5e6f3abaa4dd933069f0153a6bdfbb65d1d5ca556830a9ba5f94d7dc2&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- class 셀렉터
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/18161ab3-e447-45e9-aff5-59cf64e35d14/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T130029Z&X-Amz-Expires=86400&X-Amz-Signature=f4d2f7a63a4da0a8c825034eace5c0df6deeca946b78bdb7658baa6806ef1e83&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- id 셀렉터
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4783b9da-4a69-4818-aa2b-ece521fcde2c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T130101Z&X-Amz-Expires=86400&X-Amz-Signature=fc29df2623de80b4c4131021764cff1b891554821955fa0b35b2016a0bde9b22&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- id 셀렉터
	- id 속성의 목적은 각 태그를 유일하게 구분
		- 동일한 id 속성이 같지 않도록 HTML 파일 작성하는 것이 바람직
		- 자바스크립트 코드에서 id 값을 가진 태그 객체를 찾을 떄 문제됨
	- 적합한 활용
		- id 셀렉터는 여러 태그 중 특정 태그에만 CSS 스타일을 적용할 때 적합
- class 셀렉터
	- 적합한 활용
		- 여러 태그를 하나의 그룹으로 묶어 단체로 동일한 CSS 스타일을 적용할 때 적합
		- class 속성 값이 같은 태그에 모두 CSS 스타일 적용
	- 태그의 종류에 관계없이 class 셀렉터 활용 가능

- 셀렉터 조합하기
	- 2개 이상의 셀렉터 조합
		- 조합에 적합한 HTML 태그에만 적용
	- 자식 셀렉터
		- 부모 자식 관계인 두 셀럭터를 '>' 기호로 조합
	- 자손 셀렉터
		- 자손 관계인 2개 이상의 태그 나열
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/803ebca0-38e0-45dd-b3d1-dee4c7356af3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T130451Z&X-Amz-Expires=86400&X-Amz-Signature=cddce07fb54c2490e438485b5aae3ee339eb2ec41eecf27bd4d5716b0076232e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 전체 셀렉터
	- 와일드 문자(*)를 사용하여 모든 태그에 적용시키는 셀렉터
- 속성 셀렉터 
	- HTML 태그의 특정 속성에 대해 값이 일치하는 태그에만 스타일을 적용하는 셀렉터

- 가상 클래스 셀렉터
	- 어떤 조건이나 상황에서 스타일을 적용하도록 만든 셀렉터
		- 40개 이상의 많은 가상 클래스 셀렉터 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/174a650e-bc7f-4067-aaf4-90b6accf7356/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T130654Z&X-Amz-Expires=86400&X-Amz-Signature=c3ab5d1f0231f05046b8d3861eeb54222c2c78b4d2e67976d7090215fe074b24&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/06eb9c95-fac4-41c5-a1b5-ef99d037c268/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T130733Z&X-Amz-Expires=86400&X-Amz-Signature=a7d6746db04930dc89844d9011cf8e31fb5669da1a6601b10c927f1d8a7b89f5&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- CSS3에서 색 표현
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e4494a11-3dc0-46ef-b2cb-81bfc739513e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T130812Z&X-Amz-Expires=86400&X-Amz-Signature=8410c20e1e22ea9013a1940f6562c0d9e4362ce612ec150e83135e829d1caf26&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 색 관련 프로퍼티
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7bf471ec-4a4a-4593-920d-2a894a6fe2ad/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T130837Z&X-Amz-Expires=86400&X-Amz-Signature=cb4a0c32ba71927ddfc27db4e0b71d69dbd98c88b34ba5f49268af791b6ce5c5&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 텍스트를 꾸미는 CSS3 스타일 시트
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/fefec529-652b-4452-846e-9c6993afbaca/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T130910Z&X-Amz-Expires=86400&X-Amz-Signature=9bf96d9075dd45ddfffc992432a3ba7f163becbf5f19b1d43db20308568a1a01&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- CSS3의 표준 단위
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7fc6b4da-b0ce-4dd4-a329-1653fa79957d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T131003Z&X-Amz-Expires=86400&X-Amz-Signature=12d58c86c69e66c4a6137b82e2cc106ab2487cdda912feaf30d91350998c42ea&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 폰트
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ad5506d7-d7b7-4568-b36a-9671a95673ed/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T131038Z&X-Amz-Expires=86400&X-Amz-Signature=acead11532540bc2f449f49a0b8c9772eaae3ee23227da1e8febbef76d94fa4a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ede32352-d826-457c-9f59-bfc3e88f1128/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T131059Z&X-Amz-Expires=86400&X-Amz-Signature=93b1ecde21859eb3bc857a49f6088fad2fd3eb9480184c76dea26912cf0810ff&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/fc8760a6-f1a5-4696-8d4f-bb828a3fc168/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T131116Z&X-Amz-Expires=86400&X-Amz-Signature=c47b43f5cbaf343947706a870152e4221f819c20e7ece369a2825d2254a7332a&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 예시
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8f29ec99-7040-42a5-92e6-cddfdee6b908/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T131148Z&X-Amz-Expires=86400&X-Amz-Signature=dbca875653f5471719f0179c6ae2f80444142bb4dfda9e9a4b4486543dd51db9&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- CSS3의 박스 모델 
	- HTML 태그는 사각형 박스로 다루어짐
		- 각 HTML 태그 요소를 하나의 박스로 다룸
		- 박스 크기, 배경 색, 여백, 옆 박스와의 거리 등 제어 가능
- 박스 모델의 구성
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f4a13dc5-1a84-412b-9a8a-854ef44865a0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T131304Z&X-Amz-Expires=86400&X-Amz-Signature=3f9bdb496cbc69b744b7211c9ce45a37b32ab3dc12198c8795dfed5d2ad6ced2&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/25f09f68-2884-4861-91d8-a79ea10094d6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T131405Z&X-Amz-Expires=86400&X-Amz-Signature=5d25be4db3b05f47e0c4670910f9bdb7bdb8e0335f6081b6d87255d3963b2830&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 예시
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5fdde504-f510-43c0-b2a7-ba86b7c505f1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T131531Z&X-Amz-Expires=86400&X-Amz-Signature=6bb74dddf977cc607ff14b2275a0c179668a8e951e541b676dc27b31da568db1&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2d468e77-7c5f-42b9-85b2-076aa1eb3d93/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T131538Z&X-Amz-Expires=86400&X-Amz-Signature=c515936be05afbad7034250c59f68eb6c16b283272b2e97a47dc19f2b7313be4&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 둥근 모서리 테두리 만들기
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b087980c-d511-4f87-900a-8d8f80ec7368/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T131609Z&X-Amz-Expires=86400&X-Amz-Signature=b946afcf3f921093ee110057721b27ed8f00f208b49107a508e6224227529ba5&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 이미지 테두리 만들기
	- 테두리에 이미지를 입힘
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5f9f16cd-fa36-4436-aae7-dda613118297/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T131654Z&X-Amz-Expires=86400&X-Amz-Signature=519e5baa96726ff80f3dd6f9cf41190ed1344c341e887626f3c74946572ff031&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/54dde380-59ca-483c-b050-1630542abc1a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T131715Z&X-Amz-Expires=86400&X-Amz-Signature=1b755e6ae2cbccb522452f78299142d7c64730ae5b4e7ddb70f49484eb66d3a5&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 배경 다루기
	- 배경 색이나 이미지지정
	- 배경 이미지의 위치
	- 배경 이미지 반복 출력
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7387e749-590e-4a76-9c63-5749d4d5121d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T131834Z&X-Amz-Expires=86400&X-Amz-Signature=a170feec7258253f516b2765652f9f794e40952a899eaa4652e0f8ead213c458&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- background
	- 배경을 꾸미는 여러 값을 한 번에 지정하는 단축 프로퍼티
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c586c9e1-0f6d-4675-a4eb-65b7a0ed6af7/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T131909Z&X-Amz-Expires=86400&X-Amz-Signature=00178f9440e105c58e12a6aa60452f6be705de33401d41de7244b1e37f37fd68&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 텍스트 그림자, text-shadow
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2bfca1c0-bce3-4d24-b835-099342f36ec3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T131949Z&X-Amz-Expires=86400&X-Amz-Signature=8a2413aa42472468f444a5fffca271e57f8ef7418d39740eb02dadf21f5ec77f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7b4c64fc-9b42-4daf-ba5a-b7439a489e7d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T132012Z&X-Amz-Expires=86400&X-Amz-Signature=ee87602908b9c03484190db00653d4d4560c8290aa3704ce9493e46eb188c93b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 박스 그림자, box-shadow
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/97f930c2-840f-42a4-a329-13c95c4c4239/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T132041Z&X-Amz-Expires=86400&X-Amz-Signature=caee22e532284a8764348ad2eaf2c6aa3c47cbdef614691402fb64b07b92a1c8&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/493d0872-04a6-4009-849a-d784a131eecf/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T132103Z&X-Amz-Expires=86400&X-Amz-Signature=ca0a818450e944b0560cd095a39df93c367ed8a1a30c39bd50387a4c23d22f06&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 마우스 커서 제어, cursor
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/05716f84-dda2-42aa-926a-ab40851cb2ef/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210403%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210403T132135Z&X-Amz-Expires=86400&X-Amz-Signature=bb5a1e6d0ebf86be73c9f1eabd13189dbec29b7cb5733dcc754aa0dec6401776&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">