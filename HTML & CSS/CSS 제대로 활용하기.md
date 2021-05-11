## CSS 제대로 활용하기
- CSS에서 스타일링 할 시 요소는 선택자를 통해서 결정함
```html
<h1>Heading 1</h1>
<h2>Heading 2</h2>

<p class="important">Paragraph 1</p>
<p>Paragraph 2</p>
<p class="important">Paragraph 3</p>
<p class="important">Paragraph 4</p>
<p id="favorite">Paragraph 5</p>
<p>Paragraph 6</p>

<i>Outside</i>
<div class="div1">
  <i>Inside 1</i>
  <p>Blah blah <i>Inside 2</i></p>
  <i>Inside 3</i>
</div>

<i>Outside</i>
<div class="div1">
  <i>Inside 1</i>
  <p>Blah blah <i>Inside 2</i></p>
  <i>Inside 3</i>
</div>

<p class="one">Outside 1</p>
<p class="two">Outside 2</p>
<div>
  <p class="one">Inside 1</p>
  <p class="two">Inside 2</p>
  <p class="three">Inside 3</p>
  <p class="four">Inside 4</p>
  <p class="five">Inside 5</p>
</div>

<p class="outside one">Outside 1</p>
<p class="outside two">Outside 2</p>
<div>
  <p class="inside one">Inside 1</p>
  <p class="inside two">Inside 2</p>
  <p class="inside three">Inside 3</p>
  <p class="inside four">Inside 4</p>
  <p class="inside five">Inside 5</p>
</div>
```
```css
/* 모든 <h1> 태그 */
h1 {
  color: orange;
}

/* 'important'라는 클래스를 갖고 있는 모든 태그 */
.important {
  color: orange;
}

/* 'favorite'라는 아이디를 갖고 있는 태그 */
#favorite {
  color: blue;
}

/* 'div1' 클래스를 갖고 있는 요소의 자식 중 모든 <i> 태그 */
.div1 i {
  color: orange;
}

/* 'div1' 클래스를 갖고 있는 요소의 직속 자식 중 모든 <i> 태그 */
.div1 > i {
  color: orange;
}

/* 'two' 클래스를 가지고 있는 태그 모두와 'four' 클래스를 가지고 있는 태그 모두 선택 */
.two, .four {
  color: orange;
}

/* 'outside' 클래스를 갖고 있으면서 'one' 클래스도 갖고 있는 태그 */
.outside.one {
  color: blue;
}

/* 'inside' 클래스를 갖고 있으면서 'two' 클래스도 갖고 있는 태그 */
.inside.two {
  color: orange;
}
```

- 가상 클래스도 아래와 같이 활용가능
```html
<div class="div1">
  <p>Paragraph 1</p>
  <p>Paragraph 2</p>
  <p>Paragraph 3</p>
  <p>Paragraph 4</p>
  <p>Paragraph 5</p>
  <p>Paragraph 6</p>
</div>
```
```css
/* .div1의 자식인 <p> 태그 중 3번째 */
.div1 p:nth-child(3) {
  color: blue;
}

/* .div1의 자식인 <p> 태그 중 첫 번째 */
.div1 p:first-child {
  color: red;
}

/* .div1의 자식인 <p> 태그 중 마지막 */
.div1 p:last-child {
  color: green;
}

/* .div1의 자식 중 마지막 자식이 아닌 <p> 태그 */
.div1 p:not(:last-child) {
  font-size: 150%;
}

/* .div1의 자식 중 첫 번째 자식이 아닌 <p> 태그 */
.div1 p:not(:first-child) {
  text-decoration: line-through;
}
```

- 마우스 오버, 마우스를 올렸을 때 효과를 줌
```html
<h1>Hello World!</h1>
```
```css
h1 {
  color: orange;
}

/* 마우스가 <h1> 태그에 올라갔을 때 */
h1:hover {
  color: green;
}
```

- 상속의 개념도 존재함, 부모 요소의 속성을 자식들한테 넘겨주는 것임
- 아래와 같이 CSS 폰트 색을 파란색으로 설정하면 자동으로 다른 태그들도 파란색으로 설정이 됨
```html
<div class="div1">
  <h1>Heading 1</h1>
  <p>Paragraph bla bla bla</p>
</div>
```
```css
.div1 {
  color: blue;
}
```

- 상속되는 속성은 대표적으로 여러가지 있음
- color, font-family, font-size, font-weight, line-height, list-style, text-align, visibility
```html
<div class="div1">
  Let's go to <a href="https://google.com" target="_blank">google</a>!
</div>

<div class="div2">
  Let's go to <a href="https://google.com" target="_blank">google</a>!
</div>
```
```css
.div1 {
  color: green;
}

.div2 {
  color: orange;
}

.div2 a {
  color: inherit;
}
```

- 여러 선택자가 같은 요소를 가르키면 우선 순위는 아래와 같음
- 먼저 순서에 따라서 위에서 아래순으로 스타일을 덮어쓰는 것이 기본임
- 여기서 또 하나 구분하는 방법은 명시도에 따라서 우선 순위가 결정됨
    - 인라인 스타일이 가장 우선 순위가 높음
    - 선택자에 id가 많을수록 우선 순위가 높음
    - 선택자에 class, attribute, pseudo-class가 많을수록 우선 순위가 높음
    - 그냥 요소(또는 가상 요소)가 많은 순서

![picture](/img/HTML&CSS/CSS/one.png)

```html
<ul>
  <li><a id="link" href="#">Link 1</a></li>
  <li><a id="link" href="#">Link 1</a></li>
  <li><a id="link" href="#">Link 1</a></li>
  <li><a id="link" href="#">Link 1</a></li>
</ul>
```
```css
ul li:first-child #link {
  color: green;
}

ul li:first-child a {
  color: orange;
}
```
- CSS에서 사용하는 단위
- px → 절대적인 값, 다른 요소의 값에 영향을 받지 않음
- rem → 상대적인 값, html 태그의 font-size에만 영향을 받음
- em → 상대적인 값, 자기 자신의 font-size를 기준으로 함, 자기 자신을 따로 정해주지 않으면 상위 요소에서 상속받은 값을 기준으로 함
- % → 상대적인 값, 어느 항목에서 쓰이냐에 따라 다른 기준이 적용됨
    - font-size인 경우, 상위 요소의 font-size에 곱해주는 방식
    - margin이나 padding의 경우, 상위 요소의 width를 기준으로 계산
    - margin-top이나 padding-bottom등 세로(상하) 속성을 조절할 때에도 상위 요소인 width를 기준으로 계산