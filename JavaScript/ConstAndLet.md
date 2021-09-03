- variable을 만드는 방법은 const와 let 두개로 만듬
- 결과는 바뀌지 않음

```jsx
let a = 5;
let b = 2;
let myName = "nico";

console.log(a + b);
console.log(a * b);
console.log(a / b);
console.log("hello " + myName);
```

- 여기서 const와 let의 차이는 const는 값이 바뀔 수 없다는 것이고 variable을 바꾸는 경우 즉 업데이틀 하고 싶을 때 let을 사용해야함, 그러면 값을 바꿀 수 있음

```jsx
const a = 5;
const b = 2;
let myName = "nico";

console.log(a + b);
console.log(a * b);
console.log(a / b);
console.log("hello " + myName);

myName = "nicolas";

console.log("your new name is " + myName);
```

- 이러면 절대 바꿀 일 없는 값은 const, 바꿀 의향이 있는 것은 위처럼 let을 쓰면 됨, let은 새로운 것을 만들때만 쓰면 됨
- 만약 여기서 let이 아닌 const를 쓰면 에러가 뜸, 위처럼 업데이트가 불가능함
- 이 차이로 업데이트를 할 수 있는지 없는지 생각할 수 있음
- const를 기본적으로 사용하고 variable을 업데이트하고 싶다면 let을 씀, 몇몇 중요한 부분만 업데이트 하고 대부분 const를 쓸 것임, 필요할 때만 let을 씀
- 원래는 var을 썼음, 원할 때 업데이트 가능함 하지만 보호의 기능이 없음, 실수로 업데이트하면 값이 바뀌어 버리므로 바뀌지 않아야 하는 값도
- const는 항상 let은 가끔 var 절대 안 씀