- console.log / arrays.push 등 xx.xx 의 형태를 많이 봄
- 리스트 안에 정리하고 싶지 않을때, 어떨때는 Objects로 정리하려고 할 때도 있음
- 게임을 만든다고 할 때 Objects가 없다면 단순하게 변수로 정의해서 사용함, 근데 이것은 앞서 말한 xx.xx의 형태가 불가능함, 특성들이 한 개의 개체를 가르키기 때문에
- 데이터를 가능한 최선으로 정리하는게 필요함 → variables로만 하면 너무 불명확함, list도 별로 적절하지 않음, array는 해당 value가 무엇을 의미하는지 모름
- 물론 주석으로 말해줄 수 있으나 더 좋은 방법이 있음, 많은 variable을 만들 때
- 이 때 objects를 씀, variable과 array와 마찬가지로 선언은 같으나 차이점은 중괄호를 씀
- Objects안에서는 `=`를 쓰지않고 `:` 를 쓰고 `,` 를 통해서 property를 구분함

```jsx
const player = {
		name:"nico",
		points: 10,
		fat: true,
};
// 전체를 볼 수도 있음
console.log(player);
console.log(player.name);
```

- 이는 `console.log` 와 유사한 방식임 `[player.name](http://player.name)` 이 이는, console은 object이고 그 안의 어딘가에 log라는 것이 있는 것임
- 데이터를 정리하는 좋은 방식임, 하지만 리스트는 아님, 리스트는 모든 값이 같은 의미를 가지기 때문에

```jsx
console.log(player.name);
console.log(player["name"]); // 위와 같은 역할을 함
```

- objects를 모두 업데이트 할 수 있음, 아래와 같이

```jsx
console.log(player); // fat -> true
player.fat = false; // fat을 업데이트함
console.log(player); // fat -> false
```

- 하지만 const는 수정할 수 없는데 어떻게 된 것일까? const를 수정할 수 없는 것은 맞음 하지만 그걸 하는게 아님, 위의 과정은 object 안의 무언가를 수정한다는 것이지 const인 object 자체를 바꾸는게 아님

```jsx
player = false; // 이와 같이 처리하면 에러가 생김 const 자체를 바꾸는 것이므로
```

- objects의 무언가를 추가 하는 것은? 아래와 같이 하면 알아서 추각 됨, 어떤 property든 추가할 수 있음

```jsx
player.lastName = "potato"; // 없던 property도 추가함
```

- 아래와 같이 objects 받고 업데이트도 가능함

```jsx
const player = {
		name:"nico",
		points: 10,
		fat: true,
};

console.log(player);
player.points = players.point + 15;
console.log(player);
```