- true인지 false인지 무언가를 확인할 때 알려주는 것임, 키워드는 if
- prompt 함수는 사용자에게 창을 띄울 수 있게 함, message를 보여주고 값을 입력받게함, 이 prompt를 사용하면 JavaScript를 일시 정지 시킴, 즉 아래의 코드에서 console.log가 있어도 입력하거나 아무것도 하지 않으면 아무일도 일어나지 않음

```jsx
const age = prompt("How old are you?")

console.log(age);
```

- prompt는 잘 안 씀 스타일 상으로 바꿀 수도 없고 몇몇은 제한을함, HTML CSS를 활용함, 그저 직관적인 방법일 뿐임
- 여기서 어떤 걸 입력받더라도 type을 number로 받게 할 것임
- 위에서 받은 type은 String임
- type을 변경하기 위해서 또 다른 함수를 쓸 것임, parse를 사용
- number로 바꾸어서 비교를 할 수 있음, String은 그러한 크기 비교가 불가능함
- 만일 그냥 문자를 parse하면 NaN(Not a Number)이 뜸, 그냥 string 문자는 처리를 못함, 아래와 같이 활용 가능, 이러면 숫자를 쓰면 number로 바뀌고 문자를 입력하면 NaN이 뜸, 이렇게 구분할 수 있음

```jsx
const age = parseInt(prompt("How old are you?"));

console.log(age);
```

- 이게 NaN인지 확인하기 위해선 isNaN을 활용할 수 있음, NaN인지 아닌지, 이를 boolean을 리턴함, 만약 입력값이 NaN라면 true를 NaN이 아니라면 false를 리턴함
- condition이 true이면 그 안에 코드를 실행하고 아니면 그 안에 코드를 실행하지 않음
- 이를 응용하면 아래와 같음

```jsx
const age = parseInt(prompt("How old are you?"));

if(isNaN(age)) { // true의 경우
    console.log("Please write a number");
} else { // false의 경우
    console.log("Thank you for writing your age");
}
```

- 만약 조건이 하나 이상일 경우에는 추가를 더 할 수 있음

```jsx
const age = parseInt(prompt("How old are you?"));

if(isNaN(age)) {
    console.log("Please write a number");
} else if(age < 18) {
    console.log("You are too young.");
} else {
    console.log("You can drink");
}
```

- 조건을 여러개 걸 수도 있음
- AND 연산자, OR 연산자를 쓸 수 있음(`&&`, `||`)

```jsx
const age = parseInt(prompt("How old are you?"));

if(isNaN(age) || age < 0) {
    console.log("Please write a real positive number");
} else if(age < 18) {
    console.log("You are too young.");
} else if(age >= 18 && age <= 50) {
    console.log("You can drink");
} else if(age > 50 && age <= 80) {
    console.log("You should exercise");
} else if (age > 80) {
    console.log("You can do whatever you want");
}
```