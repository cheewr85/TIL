- JavaScript는 HTML을 인터렉티브하게 함
- console에 document를 입력하면 작성한 HTML이 보임
- documents는 HTML을 보여주지만 JavaScript에선 이를 object로 인식을 해서 접근하고 읽을 수 있게 설정됨
- 즉 JS는 HTML을 읽어옴, 그리고 가져다가 쓸 수가 있음
- object는 property를 가져오고 설정을 할 수 있음, 즉 JS에서 HTML을 변경도 할 수 있음

```jsx
document.title = "Hi" // 이렇게 하면 열었던 홈페이지의 title이 바뀜
```

- 이러한 모든 설정이 세팅되어 있음, document object를 통해서 HTML에 대해서 다 접근하고 수정할 수 있음 즉 이미 HTML에 연ㄱ결되어 있어서 데이터를 가져오고 수정할 수 있음
- document는 웹페이지를 의미함
- JS에서 HTML의 모든 항목들을 가져오고 쓸 수 있고 추가도 할 수 있음