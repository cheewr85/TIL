## Box Model
- HTML에서는 대부분 박스모델로 이루어져 있음
- 아래와 같이 박스모델이 이루어져 있음

![picture](/img/HTML&CSS/BoxModel/one.png)

- 아래와 같이 스타일 태그에서 border들 사이의 5px의 테두리를 만들게 할 수 있음

![picture](/img/HTML&CSS/BoxModel/two.png)

- 위에서 디폴트로 설정된 마진을 직접 설정할 수 있음 마진은 이 요소와 다른 요소 사이의 여백임

![picture](/img/HTML&CSS/BoxModel/three.png)

- 아래와 같이 padding을 주어서 50px만큼의 여유를 줄 수 있음

![picture](/img/HTML&CSS/BoxModel/four.png)

- 실제 박스 모델의 가로 세로 길이를 줄 수도 있음

![picture](/img/HTML&CSS/BoxModel/five.png)

- padding과 margin은 직관적으로 스타일 태그에서 줄 수 있음, 하지만 단일하게 하나의 padding으로 설정을 할 수 있음, 아래는 같은 값임, 여기서 모든 방향이 같으면 하나의 값만 위아래, 양 옆이 같으면 2개의 값만 써줘도 됨
```html
<style>
	.p1 {
		border: 5px solid red;
		padding-top: 50px;
		padding-bottom: 20px;
		padding-left: 80px;
		padding-right: 65px;
	}
</style>
```
```html
<style>
	.p1 {
		border: 5px solid red;
		padding: 50px 65px 20px 80px;
		<!-- padding: 50px 25px; -->
	}
</style>
```

- margin 역시 동일함
```html
<style>
	.p1 {
		border: 5px solid red;
		margin-top: 50px;
		margin-bottom: 20px;
		margin-left: 80px;
		margin-right: 65px;
	}
</style>
```
```html
<style>
	.p1 {
		border: 5px solid red;
		margin: 50px 65px 20px 80px;
		<!-- margin: 50px 25px; -->
	}
</style>
```

- 가운데 정렬을 위해서 왼쪽, 오른쪽 margin을 auto로 설정해주면 가운데 정렬이 됨, 위아래가 0이고 양 옆이 auto여도 동일함
- width, height → 가로 길이와 세로 길이
- width는 가로길이, height는 세로길이로 설정함
```html
<style>
	.p1 {
		border: 5px solid red;
		width: 500px;
		height: 200px;
	}
</style>
```

- min-width를 하면 적어도 500px임, 즉 웹 화면을 줄이다가 500px보다 작아지는 시점에서도 500px로 고정되어 깨져서 나옴
```html
<style>
	.p1 {
		border: 5px solid red;
		min-width: 500px;
	}
</style>
```

- max-width의 경우 500px로 고정됨 즉 화면을 아무리 늘려도 500px로 고정이 됨
```html
<style>
	.p1 {
		border: 5px solid red;
		max-width: 500px;
	}
</style>
```

- height 역시 동일하게 적용됨, 여기서 max-height를 잘못 설정하면 안의 내용이 max-height 이상으로 나타날수도 있음, 텍스트들이나 안의 내용이 서로 겹침

![picture](/img/HTML&CSS/BoxModel/six.png)

- 여기서 겹쳐서 나온 글에 대해서 처리하는 방법이 있음
- 아예 숨겨버리는 방식은 아래와 같이 처리함, 그러면 아예 잘려버림
```html
<style>
	.p1 {
		border: 5px solid red;
		max-height: 200px;
		overflow: hidden
	}
</style>
```

- 겹쳐서 보이는 것이 visible이 기본 설정값임
- 아래처럼 설정하면 스크롤을 통해서 내용을 확인할 수 있음, auto 역시 scroll할 수 있으나 scroll바가 보이지 않고 scroll은 아무리 양이 적어도 scroll바가 항상 뜸
```html
<style>
	.p1 {
		border: 5px solid red;
		max-height: 200px;
		overflow: scroll
	}
</style>
```

- 테두리를 그리는 방법은 주로 border 속성을 활용함
- 첫 번째는 테두리의 두께, 그 다음은 선의 종류, 마지막으로 색깔을 지정함

![picture](/img/HTML&CSS/BoxModel/seven.png)

- 혹은 아래와 같이 직접 정의해서 쓸 수 있음, 하지만 한 줄에 깔끔하게 쓰는 것이 좋으므로 위와 같이 씀
```html
<style>
	.p1 {
		border-style: solid;
		border-color: #4d9fff;
		border-width: 2px;
	}
</style>
```

- 서로 다른 테두리를 설정하고 싶을때 주로 다르게 정의해서 씀

![picture](/img/HTML&CSS/BoxModel/eight.png)

- 추가적으로 테두리를 없애고 싶다면 아래와 같이 활용가능
```html
<style>
	.p1 {
		border: none; <!-- border: 0; -->
	}
</style>
```

- 박스 꾸미는 몇 가지 방법
- 모서리를 둥글게 하는 방법

![picture](/img/HTML&CSS/BoxModel/nine.png)

- 요소의 배경색을 아래와 같이 색깔을 입힐 수 있음
- 색깔은 rgb값, 정해진 color값, #의 값 다 쓸 수 있음

![picture](/img/HTML&CSS/BoxModel/ten.png)

- body의 배경색과 동일하게 보이게 하기 위해서 transparent를 사용하기도 함, 아래와 같이 보임, 하지만 transparent는 기본값임, 좀 더 명확하게 해주기 위해서 쓰기도 함

![picture](/img/HTML&CSS/BoxModel/eleven.png)

- 그림자를 넣어줄 수도 있음, 기본적으로 가로세로로 가고 마이너스의 경우 그 위치가 바뀌고 그림자의 색 또한 넣어줄 수 있음, 그리고 색을 쓰기 앞에 그림자가 흐르게 나오게 하는 정도, 그림자의 크기(얼마나 퍼져야 하는지)까지 설정할 수 있음

![picture](/img/HTML&CSS/BoxModel/twelve.png)
![picture](/img/HTML&CSS/BoxModel/thirteen.png)

- box-sizing의 경우 아래와 같이 구성이 됨, 그래서 실제 내용에서 처럼 300 200으로 하고 싶으면 그만큼 값을 뺀 것을 기준으로 설정해야함

![picture](/img/HTML&CSS/BoxModel/fourteen.png)

- 실제 계산은 번거로움, 한 번에 설정하기 위해서는 아래와 같이 하면 원하는 300x200으로 설정할 수 있음, border-box를 통해서 padding과 margin이 포함됨
- 기본값은 content-box임

![picture](/img/HTML&CSS/BoxModel/fifteen.png)

- 모든 요소에 적용해서 width와 height대로 설정하고 싶다면 아래와 같이 설정하면 됨
- 모든 부분에 적용이 됨

![picture](/img/HTML&CSS/BoxModel/sixteen.png)

- 배경 이미지를 넣는 방법이 있음
- 아래와 같이 background-img를 통해서 url을 넘기면 됨
- 여기서 repeat을 하면 사진이 반복되서 나타남 꽉 채워지면서

![picture](/img/HTML&CSS/BoxModel/seventeen.png)
![picture](/img/HTML&CSS/BoxModel/eighteen.png)

- 직접 사진 크기를 정해줄 수 있음
```css
.div1 {
	height: 500px;
	border: 5px solid green;
	background-image: url("../images/beach.jpg");
	background-repeat: no-repeat;
	background-size: 100% 500px;
}
```
```css
.div1 {
	height: 500px;
	border: 5px solid green;
	background-image: url("../images/beach.jpg");
	background-repeat: no-repeat;
	background-size: cover; /* 배경을 꽉채우면서 원래 비율을 유지함 잘리는건 어쩔 수 없음*/
} 
```
```css
.div1 {
	height: 500px;
	border: 5px solid green;
	background-image: url("../images/beach.jpg");
	background-repeat: no-repeat;
	background-size: cover; /* 배경을 꽉채우면서 원래 비율을 유지함 잘리는건 어쩔 수 없음*/
	background-position: right bottom; /* 잘린 상황에서 오른쪽, 아래는 계속 유지,정렬함 */
} 
```
```css
/* 반복하지 않음 */
background-repeat: no-repeat;

/* 가로 방향으로만 반복 */
background-repeat: repeat-x;

/* 세로 방향으로만 반복 */
background-repeat: repeat-y;

/* 가로와 세로 모두 반복 */
background-repeat: repeat;

/* 반복할 수 있는 만큼 반복한 뒤, 남는 공간은 이미지 간의 여백으로 배분 */
background-repeat: space;

/* 반복할 수 있는 만큼 반복한 뒤, 남는 공간은 이미지 확대를 통해 배분 */
background-repeat: round;
```
```css
/* 원래 이미지 사이즈대로 출력 */
background-size: auto;

/* 화면을 꽉 채우면서, 사진 비율을 유지 */
background-size: cover;

/* 가로, 세로 중 먼저 채워지는 쪽에 맞추어서 출력 */
background-size: contain;

/* 픽셀값 지정 (가로: 30px, 세로: 50px로 설정) */
background-size: 30px 50px;

/* 퍼센트값 지정 (가로: 부모 요소 width의 60%, 세로: 부모 요소 height의 70%로 설정) */
background-size: 60% 70%;
```
```css
/* 단어로 지정해주기 (가로: left, center, right, 세로: top, center, bottom) */
/* 아래와 같은 총 9개의 조합이 가능 */
background-position: left top;
background-position: left center;
background-position: left bottom;
background-position: right top;
background-position: right center;
background-position: right bottom;
background-position: center top;
background-position: center center;
background-position: center bottom;

/* 퍼센트로 지정해주기 (가로: 전체 width의 25% 지점, 세로: 전체 height의 75% 지점 ) */
background-position: 25% 75%;

/* 픽셀로 지정하기 (가로: 가장 왼쪽 가장자리에서부터 오른쪽으로 100px 이동한 지점, 세로: 가장 상단 가장자리에서 아래로 200px 이동한 지점) */
background-position: 100px 200px;
```