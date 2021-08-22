- 인터페이스만으로 개발이 가능함
- 개발코드가 확연하게 줄어들고 핵심 비즈니스 로직을 개발하는데 집중할 수 있음
- 여기서 다른 부분은 앞서는 다 기본 클래스로 만들었지만 인터페이스로 Repository를 만듬
- JpaRepository에 Member 객체와 Id는 Long으로 했으니 그것을 상속받고, 앞서 만든 MemberRepository를 상속받으면됨

```java
package hello.helloworld.repository;

import hello.helloworld.domain.Member;
import org.springframework.data.jpa.repository.JpaRepository;

import java.util.Optional;

public interface SpringDataJpaMemberRepository extends JpaRepository<Member, Long>, MemberRepository {

    // 구현을 할 필요가 없음
    @Override
    Optional<Member> findByName(String name);
}
```

- 크게 구현할 요소가 없음, 그 다음 Configuration 설정을 해주면 됨
- 여기서 설정을 해주면 스프링 알아서 구현체를 만들어서 등록을 해 줌, 그걸 가져다가 쓰면 됨

```java
package hello.helloworld;

import hello.helloworld.repository.*;
import hello.helloworld.service.MemberService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration // 스프링이 configuration 먼저 읽음
public class SpringConfig {

//    // Jdbc에 연결해주기 위한 DataSource를 받아줌
//    private DataSource dataSource;
//
//    @Autowired
//    public SpringConfig(DataSource dataSource){
//        this.dataSource = dataSource;
//    }

//    private EntityManager em;
//
//    @Autowired
//    public SpringConfig(EntityManager em) {
//        this.em = em;
//    }

    private final MemberRepository memberRepository;
    // Injection만 만들어주면 SpringJPA가 만든 구현체가 자동으로 등록이 됨, 알아서 Interface만 만들어두면 구현체를 만들어냄
    @Autowired
    public SpringConfig(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }

    @Bean // Bean을 읽고 스프링빈에 등록해야 하는 것이라고 인식함
    public MemberService memberService() {
        // 그 다음 위에서 생성자로 만든 뒤 의존관계 세팅을 해줘야함
        return new MemberService(memberRepository);
    }

//    @Bean
//    public MemberRepository memberRepository() {
//        // Repository도 스프링 빈에 등록함, 여기서 Service에서 Repository의 의존관계를 주입해야하므로 바로 위에서 Service를 생성할 때 설정해줌
////        return new MemoryMemberRepository();
////        return new JdbcMemberRepository(dataSource);
////        return new JdbcTemplateMemberRepository(dataSource);
////        return new JpaMemberRepository(em);
//    }
}
```

- 즉, 스프링 데이터 JPA가 자동으로 SpringDataJpaMemberRepository를 스프링 빈으로 자동 등록해줌, 위에서 정의한 인터페이스를

![one](/img/Spring/JPA/one.png)

- JpaRepository에서 기본 메서드들을 다 제공을 해 줌, Paging, Crud까지 다 있음 Optional등등, 기본적인 모든 쿼리가 다 제공되어 있음, 단순 CRUD, 조회등, 등록 수정 삭제등이
- 그래서 그냥 가져다가 쓰면 됨, 그러므로 위에서 처럼 그대로 가져와서 쓸 수 있는 것임
- 공통화 하는 부분에 한해서는 활용가능함
- 하지만 이메일로만 찾는다던지 이름으로만 찾는다던지 하는 부분에 대해서는 공통화를 할 수 없는 부분이 있음
- 그래서 위에서 사용한 findByName의 경우도 그렇게 쓰게 된다면 자동으로 `select m from Member m where [m.name](http://m.name) = ?` 로 짬 JPQL로
- 인터페이스 이름만으로도 개발이 끝나는 것임, 단순한 구조에 대해서는 반환 타입, 메소드 이름만으로

![one](/img/Spring/JPA/two.png)
