- welcome 페이지 만들기 resources에 html 파일을 넣어두면 됨, static 정적 페이지
- 홈 화면을 만들 수 있음

![one](/img/Spring/Project/seven.png)

- 스프링 부트에서 Welcome Page를 제공함
- index.html을 static에서 찾고 못 찾으면 template에서 찾음
- 위의 index.html은 정적 페이지임, 파일을 그냥 던져준 것
- 템플릿 엔진을 통해서 동적으로 작용하게 할 수 있음
- Thymeleaf 활용
- 웹에서 가장 먼저 접근하는 부분이 Controller임
```java
package hello.helloworld.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class HelloController {

    @GetMapping("hello") // 웹 어플리케이션에서 /hello로 들어오면 아래 메소드 호출함
    public String hello(Model model) {
        // 데이터를 넘김
        model.addAttribute("data","hello!!");
        return "hello";
    }
}
```
- 그 다음 template에서 hello.html을 만듬
- 이러면 template에서 attribute로 넣음 data가 hello!로 html에서 태그를 한 것이 data가 들어감
- [localhost:8080/hello](http://localhost:8080/hello) 하면 해당 메소드가 실행이 되고 html에서 그 값이 그대로 나옴

![one](/img/Spring/Project/eight.png)

- model에 data를 넘기면서 랜더링을 하는 것

![one](/img/Spring/Project/nine.png)

### 빌드하고 실행하기

![one](/img/Spring/Project/ten.png)

- 서버를 끄고 콘솔창에서 빌드하고 실행할 수 있음
- 서버 배포시 해당 파일만 복사해서 서버에 넣어주고 실행을 시켜주면 됨