- 클릭하면 blue로 바꾸고 그 다음 다시 누를때 tomato 색깔로 바꾸는 것, 이때 앞서 사용한 이벤트여도 if 조건문이 필요함

```jsx
const h1 = document.querySelector("div.hello:first-child h1");

function handleTitleClick() {
    if(h1.style.color === "blue") {
        h1.style.color = "tomato";
    } else {
        h1.style.color = "blue";
    }
}

h1.addEventListener("click", handleTitleClick);
```

- 여기서 이를 깔끔하게 color 상태를 저장해서 할 수 있음

```jsx
const h1 = document.querySelector("div.hello:first-child h1");

function handleTitleClick() {
    const currentColor = h1.style.color;
    let newColor; // 변경 가능
    if(currentColor === "blue") {
        newColor = "tomato";
    } else {
        newColor = "blue";
    }
    h1.style.color = newColor;
}

h1.addEventListener("click", handleTitleClick);
```

- 하지만 위처럼 JS에서 style을 바꾸는 것은 여러 언어가 섞이는 것이므로 좋은 것은 아님
- 이를 먼저 CSS에 설정을 아래와 같이 해둠, 여기서 active class는 어떤 element에 지정해 주면, 어떤 element든지, h1이던, span이던 간에, tomato 색깔로 바뀜

```css
body {
    background-color: beige;
}

h1 {
    color: blue;
}

.active {
    color:tomato;
}
```

- 이제 여기서 JavaScript에서 h1에 active class를 전달해주면 됨, 아래와 같이 해주면 됨
- 직접적으로 CSS를 건드리지 않고 바꿀 수 있음

```jsx
const h1 = document.querySelector("div.hello:first-child h1");

function handleTitleClick() {
    h1.className = "active";
}

h1.addEventListener("click", handleTitleClick);
```

- 여기서 덧붙여서 한 번 더 클릭시 class name을 없애는 할 수 있는 위에서 한 것처럼 blue-tomato-blue-tomato도 할 수 있음

```jsx
const h1 = document.querySelector("div.hello:first-child h1");

function handleTitleClick() {
    if (h1.className === "active") {
        h1.className = "";
    } else {
        h1.className = "active";
    }
}

h1.addEventListener("click", handleTitleClick);
```

- 여기서 코드의 개선의 여지가 있음 active라는 String이 두 번 쓰이고 있음, 즉, 만일 저기서 active를 잘못 쓰거나 변경될 경우 제대로 동작을 하지 않음
- 이렇게 raw value, raw string을 통해서 쓰다가 실수를 내가 모르면 틀릴 수 있기 때문에 const를 생성해서 해주면 좋음, 이렇게 하면 에러가 떠도 명확하게 볼 수 있음

```jsx
const h1 = document.querySelector("div.hello:first-child h1");

function handleTitleClick() {
    const clickedClass = "active"
    if (h1.className === clickedClass) {
        h1.className = "";
    } else {
        h1.className = clickedClass;
    }
}

h1.addEventListener("click", handleTitleClick);
```

- 하지만 만약에 h1에 클래스 이름이 있다면 위와 같이 처리하면 문제가 생길 수 있음

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
        <h1 class="font">Grab Me1</h1>
    </div>
    <script src="app.js"></script>
</body>
</html>
```

```css
body {
    background-color: beige;
}

h1 {
    color: blue;
    transition: color 0.5s ease-in-out;
}

.active {
    color:tomato;
}

.font {
    font-family: 'Courier New', Courier, monospace;
}
```

- 만일 여기서 위에서 만든 JS 코드를 그대로 쓴다면 class name을 그냥 그대로 교체해버리기 때문에 문제가 생김, 이미 클래스가 있든 말든 상관을 안 쓰고 바꿔버림
- 이러면 최초의 class name이 사라져 버림, 그렇다고 이 클래스 네임을 더 추가해버리면 CSS와 JS를 계속 바뀔 때마다 써줘야 하기 때문에 비효율적임
- 여기서 JS에서 모든 class name을 변경하지 않는게 중요함, 원래 있던 class name을 지키고 변경을 하는게 중요
- 여기서 그렇게 하기 위해서 classList를 사용함, 그러면 class들의 목록으로 작업할 수 있게끔 허용해줌
- contains을 통해서 해당 클래스가 있는지 확인하고 처리할 수 있음
- classList를 사용시, element의 class 내용물을 조작하는 것이 가능함

```jsx
const h1 = document.querySelector("div.hello:first-child h1");

function handleTitleClick() {
    const clickedClass = "active"
    if (h1.classList.contains(clickedClass)) {
        h1.className = "";
    } else {
        h1.className = clickedClass;
    }
}

h1.addEventListener("click", handleTitleClick);
```

- 이렇게 하면 font 클래스가 변경되거나 건드릴 일이 없음
- 추가적으로 active라는 클래스를 제거하고 싶을 때 위와 같은 방식으로 하는게 아닌 classList 함수를 사용 가능함, 아래와 같이 그리고 추가도 가능함

```jsx
const h1 = document.querySelector("div.hello:first-child h1");

function handleTitleClick() {
    const clickedClass = "active"
    if (h1.classList.contains(clickedClass)) {
        h1.classList.remove(clickedClass);
    } else {
        h1.classList.add(clickedClass);
    }
}

h1.addEventListener("click", handleTitleClick);
```

- 이러한 작업은 매우 흔한일이고 이를 더 편리하게 해 줄 함수가 존재함
- toggle을 통해서 만약 class name이 존재하면 toggle이 class name을 제거하고 존재하지 않는다면 추가할 것임, toggle이 알아서 위의 조건문의 작업을 모두 처리해줌

```jsx
const h1 = document.querySelector("div.hello:first-child h1");

function handleTitleClick() {
    h1.classList.toggle("active");
}

h1.addEventListener("click", handleTitleClick);
```