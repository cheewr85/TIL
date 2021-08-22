- JPA를 사용하면 SQL 쿼리도 자동으로 처리해줌
- 객체 중심으로 고민을 할 수 있음, 개발 생산성도 높아짐
- JPA는 인터페이스이고 구현은 직접 해줘야함
- 객체와 ORM 기술임, 객체와 Relational DataBase를 맵핑해주는 것임
- 기존에 정의한 Member 클래스에서 애너테이션을 추가하면서 처리를 함
- 애너테이션을 가지고 DB와 맵핑하는 것임, 해당 정보를 가지고 활용함

```java
package hello.helloworld.repository;

import hello.helloworld.domain.Member;

import javax.persistence.EntityManager;
import java.util.List;
import java.util.Optional;

public class JpaMemberRepository implements MemberRepository{

    // JPA는 EntityManager로 모두 동작을 함, 자동으로 생성해서 만듬, 만들어준 것을 자동으로 만들어주므로 Injection만 해주면 됨
    private final EntityManager em;
    public JpaMemberRepository(EntityManager em) {
        this.em = em;
    }

    @Override
    public Member save(Member member) {
        // 저장을 persist로 함 아래와 같이 짜면 setId 등 모든 작업을 JPA가 알아서 처리를 해 줌
        em.persist(member);
        return member;
    }

    @Override
    public Optional<Member> findById(Long id) {
        Member member = em.find(Member.class,id);
        return Optional.ofNullable(member);
    }

    @Override
    public Optional<Member> findByName(String name) {
        // JPQL 쿼리 언어 활용, 알아서 맵핑하고 알아서 처리를 해 줌
        List<Member> result = em.createQuery("select m from Member m where m.name = :name", Member.class)
                .setParameter("name",name)
                .getResultList();

        return result.stream().findAny();
    }

    @Override
    public List<Member> findAll() {
        // JPQL 쿼리 언어를 사용해서 함, 객체를 대상으로 쿼리를 날림
        // 객체 자체를 select해서 이미 맵핑이 되어 있으므로 받아옴
        return em.createQuery("select m from Member m", Member.class)
                .getResultList();

    }
}
```

- 위와 같이 간단하게 쓸 수 있음 여기서 Serviec 객체에 항상 Transactional이 있어야함

```java
package hello.helloworld.service;

import hello.helloworld.domain.Member;
import hello.helloworld.repository.MemberRepository;
import hello.helloworld.repository.MemoryMemberRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

import java.util.List;
import java.util.Optional;

@Transactional
public class MemberService {

    // 서비스 위해 리포지토리 필요함
    private final MemberRepository memberRepository;

    public MemberService(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }

    // 회원가입 기능
    public Long join(Member member) {
        // 같은 이름이 있는 중복회원은 안됨
//        Optional<Member> result = memberRepository.findByName(member.getName());
//        // 만일 값이 이미 존재한다면, Optional을 쓰기 때문에 아래와 같이 확인해서 쓸 수 있음
//        result.ifPresent(m -> {
//            throw new IllegalStateException("이미 존재하는 회원입니다.");
//        });
        // 위의 주석처리 부분은 깔끔하지는 못함, 어차피 Optional을 반환하기 때문에 아래와 같이 쓸 수 있음, 하지만 이런건 메소드로 빼는게 좋음, 메소드로 뺌
//        memberRepository.findByName(member.getName())
//                .ifPresent(m -> {
//                    throw new IllegalStateException("이미 존재하는 회원입니다.");
//                });
        // 중복회원 검증, ExtractMethod로 뺌
        validateDuplicateMember(member);
        // 그냥 해당 멤버를 세이브해서 아이디 넘겨줌
        memberRepository.save(member);
        return member.getId();
    }

    private void validateDuplicateMember(Member member) {
        memberRepository.findByName(member.getName())
                .ifPresent(m -> {
                    throw new IllegalStateException("이미 존재하는 회원입니다.");
                });
    }

    // 전체 회원 조회
    public List<Member> findMembers(){
        return memberRepository.findAll();
    }

    // 회원 조회
    public Optional<Member> findOne(Long memberId) {
        return memberRepository.findById(memberId);
    }
}
```

- 그 다음 Configuration 설정을 해주면 됨

```java
package hello.helloworld;

import hello.helloworld.repository.*;
import hello.helloworld.service.MemberService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import javax.persistence.EntityManager;
import javax.sql.DataSource;

@Configuration // 스프링이 configuration 먼저 읽음
public class SpringConfig {

//    // Jdbc에 연결해주기 위한 DataSource를 받아줌
//    private DataSource dataSource;
//
//    @Autowired
//    public SpringConfig(DataSource dataSource){
//        this.dataSource = dataSource;
//    }

    private EntityManager em;

    @Autowired
    public SpringConfig(EntityManager em) {
        this.em = em;
    }

    @Bean // Bean을 읽고 스프링빈에 등록해야 하는 것이라고 인식함
    public MemberService memberService() {
        // 이렇게 return을 MemberService가 스프링 빈에 등록이 됨
        return new MemberService(memberRepository());
    }

    @Bean
    public MemberRepository memberRepository() {
        // Repository도 스프링 빈에 등록함, 여기서 Service에서 Repository의 의존관계를 주입해야하므로 바로 위에서 Service를 생성할 때 설정해줌
//        return new MemoryMemberRepository();
//        return new JdbcMemberRepository(dataSource);
//        return new JdbcTemplateMemberRepository(dataSource);
        return new JpaMemberRepository(em);
    }
}
```