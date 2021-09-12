- 단순히 object 차원을 떠나서 더 상세하게 해당 HTML에 있는 style까지 접근해서 바꿀 수 있음
- 그 style 안에는 다 JS 형태로 저장되어 있음
- 아래와 같이 변경 가능

```jsx
const title = document.querySelector("div.hello:first-child h1");

console.log(title);

title.style.color = "blue";
```

- h1의 style을 JS를 통해서 바꿀 수 있음, 그래서 대부분 작업할 일이, event를 listen하는 거임
- event는 마우스를 올리거나, 클릭하거나, 이름을 적거나, 와이파이 접속해제나 등등 이런 모든 일련의 과정들이 event임
- 이러한 event를 JS다 listen함
- 먼저 click event를 listen할 것임, 아래와 같이, 여기서 click을 하는 것을 listen하게 한 다음, 이를 확인하기 위해서 함수를 정의해서 동작을 하도록 했는데 이는 두 번째 인자로 넘겨주면 됨
- click event를 listen하고 function을 실행시키게 설정함, JS가 알아서 실행을 해 줌

```jsx
const title = document.querySelector("div.hello:first-child h1");

function handleTitleClick() {
    console.log("title was clicked!");
}

title.addEventListener("click", handleTitleClick);
```

- listen하고 싶은 event를 설정하고 event를 발생하면 실행할 함수를 넣어주면 됨

```jsx
const title = document.querySelector("div.hello:first-child h1");

function handleTitleClick() {
    title.style.color ="blue";
}

title.addEventListener("click", handleTitleClick);
```

- 순서를 정리하면 HTML element를 가져와서 addEventListener function을 실행시켜 주는데 이곳에 어떤 event를 listen하고 싶은지 명시해주고 왜냐하면 굉장히 많은 event들이 있기 때문에, 그리고 이 element에 해당 event를 했을 때 어떤 함수를 실행할지 설정하면 됨, function만 넘겨주면 됨
- 구글링을 한다면 매우 많은 이벤트가 있다는 것을 알 수 있음, 이를 console.dir로 알 수 있음
- 이렇게 해서 특정 event를 listen 하게 할 수 있음, 아래와 같이 추가 가능, JavaScript에 뭘 할 지 알려주고 이를 JS가 알아서 함

```jsx
const title = document.querySelector("div.hello:first-child h1");

function handleTitleClick() {
    title.style.color ="blue";
}

function handleMouseEnter() {
    title.innerText = "Mouse is here!";
}

function handleMouseLeave() {
    title.innerText = "Mouse is gone!";
}

title.addEventListener("click", handleTitleClick);
title.addEventListener("mouseenter", handleMouseEnter);
title.addEventListener("mouseleave", handleMouseLeave);
```

- 하지만 style은 CSS를 통해서만 바뀌는게 좋음
- event를 위처럼 쓰지 않고 아래와 같이도 쓸 수 있음

```jsx
const title = document.querySelector("div.hello:first-child h1");

function handleTitleClick() {
    title.style.color ="blue";
}

function handleMouseEnter() {
    title.innerText = "Mouse is here!";
}

function handleMouseLeave() {
    title.innerText = "Mouse is gone!";
}

title.onclick = handleTitleClick;
title.onmouseenter = handleMouseEnter;
title.addEventListener("mouseleave", handleMouseLeave);
```

- 하지만 addEventListener를 쓰는 이유는 나중에 removeEventListener를 통해서 제거할 수 있기 때문임
- 여기서 이제 Element가 아닌 window에 대해서도 처리를 해 줄 수 있음, 사이즈를 변경하는 순간 배경색이 바뀜

```jsx
const h1 = document.querySelector("div.hello:first-child h1");

function handleTitleClick() {
    h1.style.color ="blue";
}

function handleMouseEnter() {
    h1.innerText = "Mouse is here!";
}

function handleMouseLeave() {
    h1.innerText = "Mouse is gone!";
}

function handleWindowResize() {
    document.body.style.backgroundColor = "tomato";
}

h1.addEventListener("click", handleTitleClick);
h1.addEventListener("mouseenter", handleMouseEnter);
h1.addEventListener("mouseleave", handleMouseLeave);

window.addEventListener("resize", handleWindowResize);
```

- window에서 ctrl+c, 혹은 오른쪽 마우스 복사를 하는 순간 alert 창이 뜸

```jsx
const h1 = document.querySelector("div.hello:first-child h1");

function handleTitleClick() {
    h1.style.color ="blue";
}

function handleMouseEnter() {
    h1.innerText = "Mouse is here!";
}

function handleMouseLeave() {
    h1.innerText = "Mouse is gone!";
}

function handleWindowResize() {
    document.body.style.backgroundColor = "tomato";
}

function handleWindowCopy() {
    alert("copier!");
}

h1.addEventListener("click", handleTitleClick);
h1.addEventListener("mouseenter", handleMouseEnter);
h1.addEventListener("mouseleave", handleMouseLeave);

window.addEventListener("resize", handleWindowResize);
window.addEventListener("copy", handleWindowCopy);
```

- 이런식으로 원하는 어떤 event를 가지고 와서 처리를 할 수 있음
- element를 찾아서 event listener를 추가하고, event가 발생하면 반응을 해주는 것