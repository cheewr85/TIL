## Float
- float은 뜨게 하는 개념임
- 기본으로는 아래와 같이 구성이 되어 있음

![picture](/img/HTML&CSS/Float/one.png)

- 그 다음에 여기서 float 속성을 쓰면 아래와 같이 붕 뜨게되는 것임, 떠서 요소가 비어 있으므로 한 칸씩 아래와 같이 올라오는 것임, 사이트에서 보면 파란 div가 노란색 div를 부분적으로 덮고 있게 나옴

![picture](/img/HTML&CSS/Float/two.png)

- 실제로 보면 아래와 같이 나오게 됨, 떠 있으므로 아래와 같이 부분적으로 덮고 있음

![picture](/img/HTML&CSS/Float/three.png)

- 실제로는 아래와 같이 쓰기 위해 씀

![picture](/img/HTML&CSS/Float/four.png)

- 아래와 같이 글을 추가하면 파란색 부분이 아닌 노란색 부분에 써짐, 원래는 float으로 인해서 해당 공간이 붕 뜨고 공백이 되어 yellow div가 차지하는 것이 맞지만 inline 요소, inline-block 요소는 그 공백이 된 공간에 갈 수 없음, 즉 yellow div의 가로 길이는 100%가 맞지만 텍스트는 해당 공간을 갈 수 없음

![picture](/img/HTML&CSS/Float/five.png)
![picture](/img/HTML&CSS/Float/six.png)
![picture](/img/HTML&CSS/Float/seven.png)

- 여러 요소를 띄울 수 있음
- 기존의 float의 성질을 기준으로 아래와 같이 붕떠서 적용이 됨

![picture](/img/HTML&CSS/Float/eight.png)

- 자리를 이미 차리하고 있으면 그 옆에 자리를 잡게됨

![picture](/img/HTML&CSS/Float/nine.png)
![picture](/img/HTML&CSS/Float/ten.png)

- 이를 활용해서 Grid 레이아웃을 만들 수 있음

![picture](/img/HTML&CSS/Float/eleven.png)

- multiple floats를 활용하면 width 크기에 따라서 알아서 남은 부분을 배치함
- float 속성을 계속 활용하다보면 알아서 차곡차곡 쌓이게 됨
- clear 속성을 통해서 왼쪽에 떠있는 요소 없이 단독으로 있게끔 할 수 있음, 비우고 싶으면 clear 속성을 활용하면 됨

![picture](/img/HTML&CSS/Float/twelve.png)
![picture](/img/HTML&CSS/Float/thirteen.png)

- 에러나 오류가 나올 때 이를 해결할 수 있음
- 아래와 같은 상황에서 clear를 통해서 밑으로 내림, 그로인해 길이가 늘어나고 테두리가 정상적으로 나옴, height=0이 되는 문제, 그 다음 요소들이 영향을 받는것을 해결할 수 있음

![picture](/img/HTML&CSS/Float/fourteen.png)
![picture](/img/HTML&CSS/Float/fifteen.png)
