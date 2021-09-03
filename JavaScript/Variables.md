- JS 파일에서 console.log를 한다면 console창에 해당 값을 띄우게 함, 숫자나 문자를 넣고 콘솔에 띄울 수 있음

```jsx
console.log(5454545);
console.log("lalalala");
console.log('lalala');
```

- 하지만 위처럼 다 로그를 찍어서 연산을 한다고 하면 다 일일이 바꿀 수 없음
- 값이 바뀌면 이를 모두 다 바꿀 수 없음, 그래서 이 때 Variable을 사용하면 됨
- 이는 값을 저장하거나 유지하는 역할을 함
- const는 constant, 상수를 의미함, 값이 바뀌지 않는다는 것을 말함 계속 유지되는 것
- 변수를 쓸 때 const로 선언해서 사용함
- 이렇게 하면 한 쪽만 바꾸면 됨, 이러면 수정학기 매우 용이함

```jsx
const a = 5;
const b = 2;

console.log(a + b);
console.log(a * b);
console.log(a / b);
```

- const라는 키워드만 쓰면 variable을 쓸 수 있음, 그리고 변수명을 정하면 쓸 수 있음, 공백은 허용하지 않음, 대신 대문자로 표현을 함, 자바스크립트에선 대문자로 처리함, camel cae(파이썬은 _ 사용 → snake case)

```jsx
const name = "nico";
const veryLongVariableName = "0";

console.log("hello " + name);
```

- 이런식으로 variable을 사용하고 이를 붙이고 연산할 수 있음