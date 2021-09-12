- function의 결과를 console.log로 나오게 하는 것은 그냥 콘솔에만 띄우는 것이지 나에게 보여주는 것은 없음
- function은 무언가를 해주는 것임, 결과를 돌려주진 않음
- 이를 위해서는 다른 것을 해야함, 코드로 결과를 받아주기 위해서는 아래와 같이 처리해야함, 순수하게 결과를 얻는 것, return을 써줘야함

```jsx
const age = 96;
function calculateKrAge(ageOfForeigner) {
    return ageOfForeigner + 2;
}

const krAge = calculateKrAge(age);

console.log(krAge);
```

- 이전에 만들었던 계산기 함수를 바꿀 수 있음

```jsx
const calcultor = {
    add: function (a, b) {
        return a + b;
    },
    minus: function (a, b) {
        return a - b;
    },
    div: function (a, b) {
        return a / b;
    },
    multi: function (a, b) {
        return a * b;
    },
    power: function (a, b) {
        return a ** b;
    },
};

// variables에 value를 할당함
const plusResult = calcultor.add(5, 1);
const minusResult = calcultor.minus(plusResult , 2);
const divResult = calcultor.div(4, minusResult);
const multiResult = calcultor.multi(plusResult , minusResult);
const powerResult = calcultor.power(divResult , multiResult);
```