## HTML&CSS 시작하기
- HTML 태그(HTML 요소)
- <시작태그> 내용 <종료 태그>

![one](/img/HTML&CSS/HTML&CSS-시작하기/one.png)

- HTML 파일을 쓸 때 가장 먼저 선언하는 것, 아래와 같이 쓰면 최신 버전인 HTML5를 사용할 수 있음
```html
<!DOCTYPE html>
```

- 페이지의 제목은 <title> 태그로 씀 브라우저의 탭이나 방문 기록에 나와 있는 바로 그 제목이 들어가는 곳
```html
<title>My First Website</title>
```- <h> 태그 한 페이지에 여러 개의 머리말로 쓸 수 있는 것, 아래와 같이 중요도에 따라 크기를 서로 다르게 설정할 수 있음

```html
<h1>머리말 1</h1>
<h2>머리말 2</h2>
<h3>머리말 3</h3>
<h4>머리말 4</h4>
<h5>머리말 5</h5>
<h6>머리말 6</h6>
```

- 문단에서 사용하는 p(paragraph)태그

```html
<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
<p>Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
<p>Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
```

- 텍스트를 굵게 쓴다면 bold의 약자인 b태그 사용

```html
Hello <b>World</b>!
```

- 텍스트를 날려 쓰고 싶으면 italics의 약자인 i태그 사용

```html
Hello <i>World</i>!
```

- Phrase Tag → 단순히 시각적인 특징뿐 아니라 의미도 담고 있는 태그
- strong태그는 감싸고 있는 텍스트가 중요하다고 표시하는 것이 목적, 똑같이 굵게 보이지만 스크린리더 같은 것을 사용할 때 더 강조하여 쓸 수 있음

```html
Hello <strong>World</strong>!
```

- em태그는 i태그와 똑같은 시각적인 효과를 가지지만 강조하는 목적이 추가됨, emphasized의 줄임말임

```html
Hello <em>World</em>!
```

- 브라우저 사용시 다른 브라우저에서 한글이 깨지는 경우가 있음
- 그런 경우 meta charset="utf-8"을 추가해 그런 상황을 미연의 방지해야함

- CSS 스타일을 입히기 위해서 아래와 같이 style 태그 사용함

```html
<!-- 여기에 html 코드 -->

<style>
/* 여기에 CSS 코드 */
</style>
```

- 폰트 크기를 아래와 같이 표현할 수 있음

```html
<h1>Heading 1</h1>
<h2>Heading 2</h2>

<style>
h2 {
  font-size: 72px;
}
</style>
```

- 텍스트 정렬을 왼쪽, 가운데, 오른쪽으로 아래와 같이 할 수 있음

```html
<h1>Heading 1</h1>
<h2>Heading 2</h2>
<h3>Heading 3</h3>

<style>
h1 {
  text-align: left;
}

h2 {
  text-align: right;
}

h3 {
  text-align: center;
}
</style>
```

- 글에 색을 입히기 위해서 아래와 같이 color 속성을 활용함

```html
<h1>Heading 1</h1>
<h2>Heading 2</h2>
<h3>Heading 3</h3>

<style>
h1 {
  color: lime;
}

h2 {
  color: hotpink;
}

h3 {
  color: blue;
}
</style>
```

- margin 속성을 사용하여 요소 사이의 여백을 설정할 수 있음

```html
<h1>Heading 1</h1>
<h2>Heading 2</h2>
<h3>Heading 3</h3>

<style>
h1 {
  margin-bottom: 80px;
}

h3 {
  margin-left: 50px;
}
</style>
```

- 전체적인 구조로 묶기 위해서 아래와 같이 옵셔널 태그르 씀, 정리의 목적이 주요함

```html
<!DOCTYPE html>
<html>
	<head>
		<title>My First Website</title>
		<meta charset="utf-8">
		<style>
		  h1 {
		    font-size: 64px;
		    text-align: center;
		  }
		  
		  h3 {
		    margin-top: 100px;
		  } 
		  
		  p i {
		    font-size: 48px;
		  }
		</style>
	</head>
	<body>
		<h1>My First Page</h1>
		<h2>I <i>love</i> HTML</h2>
		<h3>안녕 세상!</h3>

		<p>Loerm ipsum <b>dolor</b> sit amet, consectetur adipiscing elit, sed do eiusmod <i>tempor</i> incididunt ut labore et dolore magna aliqua.</p>
	</body>
</html>
```

- 링크
- 하이퍼링크(anchor) → a태그 사용, blank를 통해서 새로운 탭에서 열릴 수 있게함

```html
<a href="https://google.com" target="_blank">구글로 가는 링크</a>
```

- 여기서 아래와 같이 index가 가장 상위 폴더에 있고 나머지는 하위 폴더에 있는 경우 아래와 같이 쓰면 됨
- 여기서 상위폴더로 갈때는 .. 을 활용함

```html
<!DOCTYPE html>
<html>
	<head>
		<title>My First Website</title>
		<meta charset="utf-8">
		<style>
		  h1 {
		    font-size: 64px;
		    text-align: center;
		  }
		  
		  h3 {
		    margin-top: 100px;
		  } 
		  
		  p i {
		    font-size: 48px;
		  }
		</style>
	</head>
	<body>
		<h1>My First Page</h1>
		<h2>I <i>love</i> HTML</h2>
		<h3>안녕 세상!</h3>

		<p>Loerm ipsum <b>dolor</b> sit amet, consectetur adipiscing elit, sed do eiusmod <i>tempor</i> incididunt ut labore et dolore magna aliqua.</p>

		<a href="folder1/page1.html">page 1</a>
		<a href="folder1/folder2/page2.html">page 2</a>
		<a href="folder1/folder2/page3.html">page 3</a>
	</body>
</html>
```

```html
<!DOCTYPE html>
<html>
	<head>
		<title>My First Website</title>
		<meta charset="utf-8">
		
	</head>
	<body>
		<h1>Page1</h1>
		<h2>페이지1</h2>

		<a href="../index.html">index</a>
		<a href="folder2/page2.html">page2</a>
	</body>
</html>
```

```html
<!DOCTYPE html>
<html>
	<head>
		<title>My First Website</title>
		<meta charset="utf-8">
		
	</head>
	<body>
		<h1>Page2</h1>
		<h2>페이지2</h2>

		<a href="../../index.html">index</a>
		<a href="../page1.html">page1</a>
		<a href="page3.html">page3</a>
	</body>
</html>
```

```html
<!DOCTYPE html>
<html>
	<head>
		<title>My First Website</title>
		<meta charset="utf-8">
		
	</head>
	<body>
		<h1>Page3</h1>
		<h2>페이지3</h2>
	</body>
</html>
```

- 이미지 태그를 사용하기 위해서는 아래와 같이 src의 소스를 찾아서 넣으면 됨, 그리고 속성을 활용해서 이미지 사이즈를 조정할 수 있음

```html
<img src="https://thumbor.forbes.com/thumbor/fit-in/416x416/filters%3Aformat%28jpg%29/https%3A%2F%2Fspecials-images.forbesimg.com%2Fimageserve%2F558c0172e4b0425fd034f8ba%2F0x0.jpg%3Ffit%3Dscale%26background%3D000000" width="673" height="300">
```

- 직접 가지고 있는 이미지는 아래와 같이 처리하면 됨
- 만일 상위 폴더에 있다면 ..을 사용함

```html
<img src="images/ice_cream.jpg">
<img src="../images/ice_cream.jpg width="300">
<img src="../../images/ice_cream.jpg" width="300">

```

- 여기서 이미지 정렬을 하기 위해서는 CSS 코드를 활용해야함, 아래와 같이 style 태그를 활용함

```html
<style>
	img {
		display: block;
		margin-left: auto;
		margin-right: auto;
	}
</style>
```

- 픽셀 : HTML에서 무언가의 크기를 기본적으로 픽셀 px 단위를 사용함, 화면을 구성하는 기본 단위임, 폰트 크기 역시도 픽셀 단위로 구성됨
- 길이를 픽셀 말고 퍼센트로 설정할 수도 있음