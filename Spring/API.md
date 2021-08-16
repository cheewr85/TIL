- API로 데이터로 바로 넘기는 방식임

```java
package hello.helloworld.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class HelloController {

    @GetMapping("hello-string")
    @ResponseBody // HTTP 통신 프로토콜에서 응답 Body부에 아래의 내용을 직접 넣어준다는 것
    public String helloString(@RequestParam("name") String name) {
        return "hello " + name; // name을 spring으로 넘기면 hello spring으로 그대로 넘어감
        // view없이 해당 문자가 그대로 넘어감
    }
}
```

- 아래와 같이 화면이 똑같이 떠도 페이지 소스를 보면 데이터가 그대로 나옴

![one](/img/Spring/Web/five.png)
![one](/img/Spring/Web/six.png)


- 이전 템플릿 엔진을 View를 조작하면 API는 데이터를 그대로 위처럼 보이게 함
- 문자로 하는 방식임
- 진짜는 데이터를 내놓으라고 할 때 적용이 됨

```java
package hello.helloworld.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class HelloController {

    @GetMapping("hello-api")
    @ResponseBody
    public Hello helloApi(@RequestParam("name") String name) {
        Hello hello = new Hello(); // 아래에서 만든 Hello 객체 만듬
        hello.setName(name); // setter로 넘김
        return hello; // 객체를 넘김
    }

    // 객체로 먼저 만듬, 현재 클래스에서 사용하기 위해서 static으로 선언함
    static class Hello {
        private String name;

        // 꺼낼때 getter
        public String getName() {
            return name;
        }

        // 설정할 때 setter
        public void setName(String name) {
            this.name = name;
        }
    }

```

- 이를 웹을 켜서 본다면 아래와 같이 결과가 나옴

![one](/img/Spring/Web/seven.png)

- 위와 같이 소스를 봐도 JSON 형태로 나오게 됨
- JSON은 key-value로 이루어진 구조임, key는 name, value는 spring!이 됨
- xml 방식은 HTML 태그와 같은 방식으로 됨, 이런식으로 데이터 처리를 하기도 했음
- 이젠 주로 JSON 방식으로 데이터를 처리함

![one](/img/Spring/Web/eight.png)

- 위와 같은 방식으로 처리가 됨
- hello-api를 침 → 톰켓 내장 서버에서 받아서 보냄 → helloController를 찾음
- 여기서 ResponseBody라는 애너테이션이 존재함, 이 애너테이션이 없으면 viewResolver에서 나한테 맞는 템플릿에게 던지는데 애너테이션이 있으면 Http 응답에 넣었을 때 객체가 오면 JSON방식으로 데이터를 만들어서 HTTP응답에 반환을 함
- 해당 객체를 보고 HttpMessageConverter가 동작을함 → 단순 문자면 StringConverter가 작용해 String으로 바꾸고 객체라면 JSONConverter가 적용을 해서 JSON으로 바꿈
- 객체를 name이 있고 값이 있으면 JSON 스타일로 바꾸고 바꾼걸 요청한 서버든 웹브라우저든 거기에 보냄
- XML 라이브러리를 추가한다면 XML로써도 처리를 할 수 있음