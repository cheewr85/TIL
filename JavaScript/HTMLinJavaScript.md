- 특정한 어떤 것을 가져오는 것을 가져올 수 있음, 먼저 아래와 같이 HTML을 만든 뒤에 document 객체와, element를 가져오는 수 많은 함수들을 이용함

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
    <h1 id="title">Grab me!</h1>
    <script src="app.js"></script>
</body>
</html>
```

- 위의 id를 가져오기 위해서 document에 접근해서 가져올 수 있음, 해당 태그를 그대로 가져올 수 있음

```jsx
document.getElementById("title");
```

- element를 자세히 보기 위해서 dir을 사용할 수 있음, 그러면 h1 태그에 대한 자세한 내용을 다 볼 수 있음

```jsx
const title = document.getElementById("title");

console.dir(title);
```

- 중요한 것은 HTML을 표현하는 object를 JavaScript로 가져와서 볼 수 있는 것임, 위처럼 console.dir등을 써서
- 똑같은 element를 JavaScript를 통해서 보는 것, 그리고 이러한 것을 바꿀 수도 있음

```jsx
const title = document.getElementById("title");

title.innerText = "Got you!";
```

- 즉, HTML에 의해서 바꾼게 아니라 JS에서 element를 가져와서 바꾼 것임
- 이는 모든 HTML 과 관련된 것에 접근해서 건드릴 수 있다는 것을 말함
- 이런식으로 HTML에서 항목들을 가지고 와서 JavaSctipt를 통해 항목들을 변경할 것임
- JS에서 어떤 HTML Element를 가져올 수 있음, 그리고 원하는 무엇이든 할 수 있음