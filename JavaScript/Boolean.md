- variables안에 저장할 수 있는 데이터 타입 boolean
- true 아니면 false임, 마치 0과 1과 같이, 따옴표로 감싸면 안됨 그건 문자임

```jsx
const amIFat = true;
console.lof(amIFat);
```

- true 인지 false인지만 중요함, 데이터 타입임
- 존재하지 않는 것, 그 변수에 아무것도 없다는 것을 null 이라고 함 아무것도 아님, false랑 다름
- 말 그대로 아무것도 아닌 것, 데이터 타입임

```jsx
const amIFat = null;
console.log(amIFat);
```

- 존재하지 않는, 아무것도 아닌, 존재하지 않는 것, 즉 아무 값도 주지 않는 것 undefined라고 뜸 그러면 데이터 타입임

```jsx
let something;
```

- variable을 존재하지만 값을 안 준 것 undefined임, 메모리 안에 공간이 있지만 값이 들어가지 않은 것
- null은 절대 자연적으로 발생하지 않음, null은 variable안에 어떤 것이 없다는 것을 확실히 하기 위해 쓰는 것임, 여기엔 값이 없다는 것을 알려줄 때 쓰는 것임, 의도적으로 비어있음을 표현함
- undefined는 어떤 variable이 메모리에는 있는데 값이 없는것임