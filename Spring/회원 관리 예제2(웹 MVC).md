## 홈 화면 추가
- 홈 화면을 만들어서 처리하기 위해서 컨트롤러를 만듬

```java
package hello.helloworld.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class HomeController {
    // 홈화면에 대한 리턴을 할 것임

    @GetMapping("/") // 도메인 첫번째를 의미함
    public String home() {
        return "home";
    }
}
```

- 그리고 그에 맞는 template html 파일을 만듬
```html
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<body>
<div class="container">

    <div>

        <h1>Hello Spring</h1>

        <p>회원 기능</p>

        <p>

            <a href="/members/new">회원 가입</a>

            <a href="/members">회원 목록</a>

        </p>

    </div>
</div> <!-- /container -->
</body>
</html>
```
- 여기서 알아둬야 할 부분은 요청이 오면 스프링 컨테이너에서 컨트롤러를 찾고 그 다음 없다면 template을 찾음
- 위의 경우는 컨트롤러가 있고 바로 찾은 거고 맵핑한거로 넘어간거고 static은 무시됨

## 등록
- 이전에 만들었는 MemberController 활용함
- 만든 HTML 파일에선 등록은 members/new로 가므로 그쪽에 맵핑을 해야함
- 이와 관련된 HTML을 template으로 만들고 그 다음 처리를 함

```html
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<body>
<div class="container">

  <form action="/members/new" method="post">

    <div class="form-group">

      <label for="name">이름</label>

      <input type="text" id="name" name="name" placeholder="이름을
입력하세요">

    </div>

    <button type="submit">등록</button>

  </form>
</div> <!-- /container -->
</body>
</html>
```

- 이러면 name이라는 key와 내가 입력한 값을 value로 넘어와서 저장됨
- 회원등록을 하는 Controller 역시 만들어야함
- 아래와 같이 만들면 위에서 HTML로 만든 name이랑 아래에서 만든 controller의 name이 매칭이 됨

```java
package hello.helloworld.controller;

public class MemberForm {
        // 회원등록 페이지에서 등록하면 받은 값 넘기기
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

- 그 다음 MemberController에서 PostMapping을 통해서 위에서 만든 Form을 연결해줘야함

```java
package hello.helloworld.controller;

import hello.helloworld.domain.Member;
import hello.helloworld.service.MemberService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;

@Controller
public class MemberController {

    // new로 객체를 새로 만들지 않고 한 번만 컨테이너에 넣어서 여기저기서 쓰면 됨 그러기 위해서 생성자를 통해서 만듬
    private final MemberService memberService;

    @Autowired // 스프링 컨테이너에 MemberController를 둘 때 생성자에 이 애너테이션을 쓰면 memeberService를 스프링이 스프링컨테이너에 있는 memberService를 가져다가 씀
    public MemberController(MemberService memberService) {
        this.memberService = memberService;
    }

    @GetMapping("members/new")
    public String createForm() {
        return "members/createMemberForm";
    }
    
    @PostMapping("members/new")
    public String create(MemberForm form) {
        // member에 대한 객체를 만들어서 만듬
        Member member = new Member();
        // set을 하는데 MemberForm에 있는 걸로 set을 함
        member.setName(form.getName());
        // 이를 memberservice에 join을 함
        memberService.join(member);
        // 회원가입이 끝났으므로 홈화면으로 보냄
        return "redirect:/";
    }
}
```

- join을 통해서 알아서 잘 들어가 있을것임
- 회원가입 → members/new로 들어감(GET 방식으로) →  createForm은 return을 템플릿에 있는 createMemberForm이라는 것으로 보냄 → 그럼 해당 html을 뿌려주는 것임 → input을 통해서 텍스트를 입력할 수 있게 함 → 등록 버튼을 누르면 action url → members/new에서 PostMapping으로 넘어옴 → 그 다음 create 메소드가 처리됨 → 값이 들어옴 MemberForm에서 입력한 값이 들어옴(name에) → 그 다음 그 name을 getName으로 꺼내고 join을 통해서 그 값이 등록이 됨

## 조회
- 이전에 Controller에서 GetMapping으로 추가를 함

```java
@GetMapping("/members")
    public String list(Model model) {
        // memberService에서 정의함 다 가져올 수 있음 Member를
        List<Member> members = memberService.findMembers();
        model.addAttribute("members", members); // model Attribute에 담아서 다 넘겨줄 것임 받은 데이터를
        return "members/memberList";
    }
```

- 그 다음 해당 template을 추가함

```html
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<body>

<div class="container">
  <div>
    <table>
      <thead>
      <tr>

        <th>#</th>

        <th>이름</th>

      </tr>

      </thead>

      <tbody>

      <tr th:each="member : ${members}">

        <td th:text="${member.id}"></td>

        <td th:text="${member.name}"></td>

      </tr>

      </tbody>

    </table>

  </div>
</div> <!-- /container -->
</body>
</html>
```

- 여기서 본격적인 작업은 tr에서 함
- members를 읽어주는데 컨트롤러에서 members라는 것을 model에 attribute를 추가함, 즉 위처럼 HTML 태그에서 members를 루프를 돌면서 List에 있는 회원목록을 나타내는 것임
- 여기서 인텔리제이를 끄면 다시 데이터가 다 초기화 됨, 여기서 DB에 넘겨서 저장해야함