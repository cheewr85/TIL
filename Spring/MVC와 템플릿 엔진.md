- MVC: Model, View, Controller
- 예전에는 View에다가 모든걸 다 했지만 요즘엔 MVC로 많이함
- View는 화면을 그리는데 모든 역량을 집중해야함, Controller나 Model은 내부 비즈니스과 관련있거나 로직을 처리하는데 집중을 함
- Controller와 View를 쪼개는게 흔함

```java
package hello.helloworld.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
public class HelloController {

    @GetMapping("hello-mvc")
    // 외부에서 파라미터를 받기 위해서 Param을 받음
    public String helloMvc(@RequestParam("name") String name, Model model) {
        // 파라미터로 넘어온 name을 추가함
        model.addAttribute("name",name);
        return "hello-template";
    }
}
```

- 여기서 HTML을 아래와 같이함, p 태그 안 내용은 상관이 없음, 알아서 th로 치환됨, 서버없이 HTML 만들때 쓰기 위해서 안 내용을 쓰는 것, 실제 서버를 타면 내용이 바뀜

```html
<html xmlns:th="http://www.thymeleaf.org">
<body>
<p th:text="'hello ' + ${name}">hello! empty</p>
</body>
</html>
```

- 여기서 localhost와 함께 해당 값을 보내줘야함, 아래와 같이

![one](/img/Spring/Web/three.png)

- 위처럼 처리하면 파라미터로 spring!을 넘겨줘서 HTML에서의 모델에서 그 값을 치환해서 넘겨줌

![one](/img/Spring/Web/four.png)

- 위처럼 내장 톰켓 서버를 하고 helloController를 불러오고 return 시 viewResolver에서 templates에서 hello-template과 똑같은 것을 찾아서 Thymeleaf 템플릿 엔진 처리를 하게끔 함
- 그 다음 HTML이 렌더링 한 후 변환해서 웹브라우저에 넘겨줌, 그래서 name부분이 변환이되서 넘어감