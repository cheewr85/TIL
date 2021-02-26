## Viewcomponent
- setContentView -> 레이아웃 화면만을 띄우고 싶다면 해당 레이아웃을 나타내면 됨
- Viewcomponent는 화면을 그리는 요소임, 각종 버튼과 UI 부분
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/50209538-3690-4976-b230-837df9cc9b4f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210226%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210226T102918Z&X-Amz-Expires=86400&X-Amz-Signature=098d727c1d37f5d1c66000a838d3eb18bbf1995b5ccfdf33e750c9d4655b684f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 위를 활용하여서 드래그 앤 드랍으로 만들 수 있음, 하지만 매우 어려운 방식이므로 xml 코드를 직접 작성하는 것이 좋음
- Viewcomponent의 종류를 확인할 때 Design 탭을 사용하면 좋음
- xml은 Viewcomponent를 적을 때 여는 꺽새 '<'로 시작 -> Viewcomponent의 종류 -> 그리고 '/>'전까지 속성들을 적음, '</TextView>' 로 끝낼수도 있음
- Viewcomponent들은 서로 부모-자식 관계를 가질 수 있음, 자동으로 들여쓰기가 됨 
- Viewcomponent의 속성을 가지고 많은 것들을 설정할 수 있음 -> 이러한 다양한 속성을 Design탭의 해당 View의 다양한 속성을 확인할 수 있음 -> xml 코드로 설정한 것을 Declared Attributes를 통해서 확인할 수 있음
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/61a65d2a-b0ec-4db2-a3d3-5bf36859322f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210226%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210226T103217Z&X-Amz-Expires=86400&X-Amz-Signature=40fd584df19aa45755e5d831f45e0869f8b9db1c6d6923f87c9308aee3b963bf&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- All Attributes는 해당 View가 사용할 수 있는 모든 속성이 들어가 있음, 이를 통해 속성을 알 수 있음