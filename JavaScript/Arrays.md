- 데이터를 정리하는 방법
- 삽입 검색 등 데이터를 어떻게 효과적으로 정렬할 것인지 자료구조를 씀
- 가장 기본적인 것이 배열(Arrays)임
- 만약 쓰지 않고 쓴다면 아래와 같이 그냥 나열을 함

```jsx
const mon = "mon";
const tue = "tue";
const wed = "wed";
const thu = "thu";
const fri = "fri";
const sat = "sat";
const sum = "sun";
```

- 이를 리스트로 그룹화 한다면 완전 날 것 그대로 생각하면 매우 크고 긴 variable로 생각을 할 수가 있음

```jsx
const dayOfWeek = mon + tue + wed + thu + fri + sat + sun;
```

- 위처럼 하면 그냥 긴 String이 될 뿐임
- 무언가를 나열하기 위해 데이터를 그룹으로 묶는 좋은 방법이 있음 → array 사용

```jsx
const dayOfWeek = [mon, tue, wed, thu, fri, sat, sun];
```

- array에 어떻게 든 담아서 확인할 수 있음, 이를 console에 찍으면 어떻게 담겼는지 다 확인할 수 있음

```jsx
const nonsense = [1, 2, "hello", false, null, true, undefined, "nico"];

console.log(daysOfWeek, nonsense);
```

- 규칙은 시작과 끝을 대괄호를 쓰고 요소들을 쉼표로 구분을 하면 됨
- 위에서처럼 변수가 아닌 그냥 문자열을 넣어서 할 수 있음
- 그리고 숫자를 세듯이 논리적으로 어떤 위치를 찾고 싶은지에 대해서 array안의 데이터를 접근하고 싶다면 variable이름과 대괄호와 얻고 싶은 항목의 번호를 찾으면 됨, 컴퓨터는 0부터 세는걸 알고 시작해야함

```jsx
const dayOfWeek = ["mon", "tue", "wed", "thu", "fri", "sat"];

console.log(daysOfWeek[4]); // fri 출력(4번째)
```

- 더 많은 것을 할 수 있음, array에 하나 더 추가할 수도 있음
- 많은 것들을 사용할 수 있음 그 중 추가하는 것인 push만 쓸 것임

```jsx
const dayOfWeek = ["mon", "tue", "wed", "thu", "fri", "sat"];

// -> 주석 
// Get Item from Array
console.log(daysOfWeek[4]); // fri 출력(4번째)

// Add one more day to the array
daysOfWeek.push("sun");

console.log(daysOfWeek); // sun이 추가되어 있음
```