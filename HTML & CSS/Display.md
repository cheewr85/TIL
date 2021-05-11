## Display
- display 속성
- 여러가지 display 속성을 태그들은 가지고 있음, 주로 아래와 같음

![picture](/img/HTML&CSS/Display/one.png)
![picture](/img/HTML&CSS/Display/two.png)
![picture](/img/HTML&CSS/Display/three.png)

- 각 요소는 기본적으로 정해져 있는 display가 있음, 직접 CSS 코드를 통해서 display를 바꿀 수 있음
- block 요소는 항상 100%를 차지하지 않음, 직접 width, height를 설정해주면 그만큼만 차지함, inline 요소는 그렇지 않음, 안에 내용물에 따라 다름
- 같은 줄에 머물면서 가로,세로 길이 block처럼 설정하는 법 → inline-block
- inline-block 요소는 inline처럼 같은 줄에 머무르면서 width, height를 block처럼 조절할 수 있음
- img 태그는 같은 줄에 있으면서 가로,세로를 설정할 수 있음, inline display임, inline임에도 img는 가로 세로를 설정할 수 있음, 텍스트처럼 활용할 수 있음(텍스트 스타일링 사용 가능), 엄청 큰 글자라고 생각, 글자처럼 다룰 수 있음
- 주로 이미지를 정렬은 아래와 같이 함
```css
img {
	display: block;
	margin-left: auto;
	margin-right: auto;
}

/* 만일 위와 같이 하지 않으면 아래와 같이 부모요소를 통해서 정렬해야하지만 부자연스러움*/

.container {
text-align: center;
}
```
- 다양한 링크 → 링크인 a 태그에서 글이 아닌 이미지로도 설정해서 할 수 있음

![picture](/img/HTML&CSS/Display/four.png)
![picture](/img/HTML&CSS/Display/five.png)
![picture](/img/HTML&CSS/Display/six.png)

- 박스끼리 정렬은 되어 있지 않지만 텍스트들이 기본적으로 baseline에 맞춰서 아래와 같이 정렬이 됨, 텍스트 바로 밑이 baseline임

![picture](/img/HTML&CSS/Display/seven.png)
![picture](/img/HTML&CSS/Display/eight.png)

- 아래와 같이 나오게 된다면 요소의 마지막 부분에 대해서 baseline이 설정됨

![picture](/img/HTML&CSS/Display/nine.png)

- 하지만 아래와 같이 요소가 하나도 없으면 박스의 맨 아래로 baseline이 그냥 설정됨

![picture](/img/HTML&CSS/Display/ten.png)

- 그리고 박스가 작아지더라도 아래와 같이 요소의 마지막에 대해서 baseline이 생성됨

![picture](/img/HTML&CSS/Display/eleven.png)

- 하지만 여기서 overflow 설정을 다르게 scroll, visible로 설정한다면 baseline 설정이 달라짐

![picture](/img/HTML&CSS/Display/twelve.png)

- 아래와 같이 박스모델을 생성하게 되면 vertical-align 속성을 baseline으로 설정되어 있음 span에서의 요소의 baseline을 부모 요소에 맞추게끔 하는 것임

![picture](/img/HTML&CSS/Display/thirteen.png)
![picture](/img/HTML&CSS/Display/fourteen.png)

- 여기서 vertical-align 속성을 건드려서 top으로 두면, 위의 배치한 것 중 가장 높은 요소에 맞춰서 배치가 됨

![picture](/img/HTML&CSS/Display/fifteen.png)

- 근데 alex를 건드리게 되면 아래와 같이 좀 다른 모양이 나옴
- 즉, alex를 제외하고 제일 높은 것에 baseline을 맞추는데 그러면 chris를 기준으로 움직이고 여기서 chris를 기준으로 baseline을 맞추면 자연스럽게 ben과 x도 chris에 맞게 맞춤
- baseline은 고정된 것이 아닌 상황에 따라 움직일 수 있는 요소들임

![picture](/img/HTML&CSS/Display/sixteen.png)

- 여기서 추가적으로 ben에게 vertical-align을 middle을 주면 부모 요소로 사용되는 x에 가운데를 맞춰서 ben에 가운데가 맞춰짐

![picture](/img/HTML&CSS/Display/seventeen.png)

- 여기서 chris에게 middle을 주면 alex는 baseline을 middle로 맞추지 않았기 때문에 부모요소 자체가 아래와 같이 조금 늘어나게 됨

![picture](/img/HTML&CSS/Display/eighteen.png)

- 모든 요소를 가운데로 맞추기 위해서는 아래와 같이 모든 요소를 맞추면 됨

![picture](/img/HTML&CSS/Display/nineteen.png)

- 간단하게 가로 가운데 정렬의 경우 아래와 같이 구분할 수 있음
- inline 요소
```html
<div class="container">
  텍스트 <img src="https://i.imgur.com/CDPKjZJ.jpg" height="50">
</div>
```
```css
.container {
  text-align: center;
  background-color: lime;
}
```

- block 요소
```html
<div class="block-element"></div>
```
```css
.block-element {
  width: 100px;
  height: 50px;
  margin-left: auto;
  margin-right: auto;
  background-color: lime;
}
```

- 세로 가운데 정렬
- vertical-align middle을 사용하는것이 방법이지만, 그 전에 이 요소는 inline, inline-block에서만 적용되기 때문에 그 설정을 바꾸어야 함
- 아래와 같이 적용을 해보면 가운데에 위치함을 알 수 있음
```html
<div class="container">
  x
  <div class="helper"></div>
  <div class="info">
    <h1>Hello!</h1>
    <p>My name is young.</p>
  </div>
</div>
```
```css
.container {
  width: 300px;
  height: 400px;
  background-color: gray;
  text-align: center;
}

.helper {
  display: inline-block;
  height: 100%;
  vertical-align: middle;
  
  /* 설명을 위해서 */
  width: 10px;
  background-color: red;
}

.info {
  background-color: lime;
  display: inline-block;
  vertical-align: middle;
}
```

- 하지만 위에서 .info를 width를 100%로 하면 이상한 곳에 위치함, 즉 자리부족으로 다음 줄로 가버리는 것임
- 이를 해결하기 위해서 띄어쓰기를 아래와 같이 없애거나
```html
<div class="container">
  <!-- 스페이스 없애기 -->
  <div class="helper"></div><div class="info">
    <h1>Hello!</h1>
    <p>My name is young.</p>
  </div>
</div>
```

- 띄어쓰기 공간만큼의 마이너스 여백을 주면 됨
```css
.container {
  width: 300px;
  height: 400px;
  background-color: gray;
  text-align: center;
}

.helper {
  display: inline-block;
  height: 100%;
  vertical-align: middle;
}

.info {
  background-color: lime;
  display: inline-block;
  vertical-align: middle;
  width: 100%;

  /* 이 경우 띄어쓰기는 5~7px 정도였습니다! */
  margin-left: -7px;
}
```

- 또 다른 방법으로는 line-height를 아래와 같이 주어서 해결할 수 있음
```css
.container {
  width: 300px;
  height: 400px;
  background-color: gray;
  text-align: center;
  line-height: 400px;
}

.info {
  background-color: lime;
  display: inline-block;
  line-height: normal;
  vertical-align: middle;
}
```