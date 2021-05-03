## Viewcomponent
- setContentView -> 레이아웃 화면만을 띄우고 싶다면 해당 레이아웃을 나타내면 됨
- Viewcomponent는 화면을 그리는 요소임, 각종 버튼과 UI 부분
![one](/img/Android/UI/Viewcomponent/first.png)

- 위를 활용하여서 드래그 앤 드랍으로 만들 수 있음, 하지만 매우 어려운 방식이므로 xml 코드를 직접 작성하는 것이 좋음
- Viewcomponent의 종류를 확인할 때 Design 탭을 사용하면 좋음
- xml은 Viewcomponent를 적을 때 여는 꺽새 '<'로 시작 -> Viewcomponent의 종류 -> 그리고 '/>'전까지 속성들을 적음, '</TextView>' 로 끝낼수도 있음
- Viewcomponent들은 서로 부모-자식 관계를 가질 수 있음, 자동으로 들여쓰기가 됨 
- Viewcomponent의 속성을 가지고 많은 것들을 설정할 수 있음 -> 이러한 다양한 속성을 Design탭의 해당 View의 다양한 속성을 확인할 수 있음 -> xml 코드로 설정한 것을 Declared Attributes를 통해서 확인할 수 있음
![two](/img/Android/UI/Viewcomponent/second.png)

- All Attributes는 해당 View가 사용할 수 있는 모든 속성이 들어가 있음, 이를 통해 속성을 알 수 있음