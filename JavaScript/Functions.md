- function은 계속 반복해서 사용할 수 있는 코드 조각임
- 가능한 적은 코드를 적고 싶어함, 어떠한 이름을 Hello 해주는 function을 만들어봄
- 만약 function을 하지 않으면 계속해서 반복해서 복붙하고 바꿔야함

```jsx
console.log("Hello my name is Nico");
console.log("Hello my name is Dal");
console.log("Hello my name is Shigatsu");
console.log("Hello my name is Nico");
console.log("Hello my name is Nico");
console.log("Hello my name is Nico");
```

- 위의 방식은 좋은게 아님, 코드의 반복을 최소한 줄이는게 좋음, 이때 function을 만듬, function은 어떤 코드를 캡슐화해서, 실행을 여러 번 할 수 있게 해줌
- 만들 때 말그대로 function을 일단 붙이면 됨, 몇 가지 규칙이 있는 데 아래와 같이 기본틀은 만들어야 함

```jsx
function sayHello() {
	// 여기다가 함수 작성(계속 반복 할 수 있음)
	console.log("Hello!");
}

// () 실행버튼과 같은 느낌
sayHello();
sayHello();
sayHello();
sayHello();
```

- function이 위와 같은 것은 똑같은 방법을 하는데 이를 바꿀 수 있음, 안의 내용 arguments(인수)를 받아서 정보를 function에 전달해서 바꾸는 것임 `()` 에 넣어서 보내서 쓰면 됨
- 하지만 여기서 데이터를 보내고 데이터가 읽어야 하는 방법은 아래처럼 추가해야함 보내는 것은 `()` 안에 넣어서 보내면 됨
- 즉, 받기 위해선 함수 `()` 안에 넣으면 됨, 그리고 이를 활용하여서 쓰면 됨 아래와 같이, 여기서 이러한 argument는 여러개 넣을 수 있음, 이는 함수 body 안에만 존재함

```jsx
function sayHello(nameOfPerson, age) { // argument 데이터를 받음
	console.log("Hello my name is " + nameOfPerson + " and I'm " + age);
}

sayHello("nico", 10);
sayHello("dal", 23);
sayHello("lynn", 21);
```

- 받을 argument 이름과 상관없이, 순서에 맞춰서 들어감을 알아야 함
- 아주 간단한 계산기 예시

```jsx
function plus(firstNumber, secondNumber){
    console.log(firstNumber + secondNumber);
}
function divide(a, b) {
    console.log(a / b);
}
plus(8, 60);
divide(98, 20);
```

- object에도 활용해서 할 수 있음, 함수를 넣어서

```jsx
const player = {
    name: "nico",
    sayHello: function() {
        console.log("hello!");
    },
};

console.log(player.name);
player.sayHello(); // console.log와 유사함
```

- arguments를 넣어서 활용 가능, 아래와 같이

```jsx
const player = {
    name: "nico",
    sayHello: function(otherPersonName) {
        console.log("hello " + otherPersonName + " nice to meet you!");
    },
};

console.log(player.name);
player.sayHello("lynn");
```

- 계산기 예시

```jsx
const calcultor = {
    add: function (a, b) {
        console.log(a + b);
    },
    minus: function (a, b) {
        console.log(a - b);
    },
    div: function (a, b) {
        console.log(a / b);
    },
    multi: function (a, b) {
        console.log(a * b);
    },
    power: function (a, b) {
        console.log(a ** b);
    },
};

calcultor.add(5, 1);
calcultor.minus(3, 2);
calcultor.div(4, 7);
calcultor.multi(5, 2);
calcultor.power(2, 8);
```