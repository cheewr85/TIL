- HTML에 정의된 id가 JavaScript에서 같으면 찾을 수 있음, 어떻든 간에
- 만약 class name이 정의된 태그가 5개가 아래와 같이 있다고 가정

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="style.css">
    <title>Momentum App</title>
</head>
<body>
    <h1 class="hello">Grab me!</h1>
    <h1 class="hello">Grab me!</h1>
    <h1 class="hello">Grab me!</h1>
    <h1 class="hello">Grab me!</h1>
    <h1 class="hello">Grab me!</h1>
    <script src="app.js"></script>
</body>
</html>
```

- 여기서 class Name을 확실하게 해서 JS를 통해서 얻을 수 있음
- 많은 elements를 가져오려곡 할 때 ClassName을 통해서 가져오면 됨, 아래와 같이 불러온다면 위의 5개의 태그에 대해서 모두 불러올 수 있음

```jsx
const hellos = document.getElementsByClassName("hello");

console.log(hellos);
```

- 하지만 className이 없는게 있을 수 있음, 만약 아래와 같이 HTML이 존재한다면

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="style.css">
    <title>Momentum App</title>
</head>
<body>
    <div class="hello">
        <h1>Grab Me!</h1>
    </div>
    <script src="app.js"></script>
</body>
</html>
```

- 우선 생각할 수 있는건 TagName을 가져와서 쓸 수 있음, 하지만 이는 모든 해당 태그를 가져오는거dla

```jsx
const title = document.getElementsByTagName("h1");
```

- 그래서 좀 더 세련된 방식은 querySelector를 사용하는 것임, 이는 element를 CSS 방식으로 검색할 수 있는것임
- CSS selector를 사용해서 class hello를 찾고 그 안에 h1 태그를 찾을 수 있음

```jsx
const title = document.querySelector(".hello h1");

console.log(title);
```

- CSS 방식임, 그래서 hello가 class name이라는 것과 그 안의 h1을 명시해줘야함, 위에서 단순하게 tag name을 가지고 간 것과는 다르게
- 단 하나의 element만을 return 해 줌
- 만약 아래와 같이 여러개가 있다면

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="style.css">
    <title>Momentum App</title>
</head>
<body>
    <div class="hello">
        <h1>Grab Me1</h1>
    </div>
    <div class="hello">
        <h1>Grab Me2</h1>
    </div>
    <div class="hello">
        <h1>Grab Me3</h1>
    </div>
    <script src="app.js"></script>
</body>
</html>
```

- 똑같이 JS 코드를 쓴다면 첫번째 것 하나만 나옴, 많은 hello h1이 존재할수도 있음, 하지만 querySelector는 첫번째 element만 가져옴

```jsx
const title = document.querySelector(".hello h1");

console.log(title);
```

- 만약 이를 다 가져오고 싶다면 아래와 같이 써야함

```jsx
const title = document.querySelectorAll(".hello h1");

console.log(title);
```

- id 역시 querySelector를 통해서 찾을 수 있음, id 하위에 있는것도 가져올 수 있음

```jsx
const title = document.querySelector("#hello");
// 아래와 같은 의미임
const title = document.getElementById("hello");
```