- 이전에 한 순수 Jdbc와 동일한 환경설정을 함
- 여기서 라이브러리는 JDBC API에서 본 반복 코드를 대부분 제거해줌, SQL은 직접 작성해줘야함
- MemberRepository를 implements하는 작업은 동일함
- 그 전에 사전 작업은 아래와 같이 함

```java
// JdbcTemplate을 먼저 받음
    private final JdbcTemplate jdbcTemplate;

    // Injection 하는 작업 datasource를 넣어줌, 이전에 생성자와는 살짝 다름
    @Autowired // 생성자가 딱 하나 있다면 Autowired를 생략할 수 있음
    public JdbcTemplateMemberRepository(DataSource dataSource){
        jdbcTemplate = new JdbcTemplate(dataSource);
    }
```

- 아래와 같이 각각 기능에 대해서 간단하게 구현을 할 수 있음

```java
package hello.helloworld.repository;

import hello.helloworld.domain.Member;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.jdbc.core.RowMapper;
import org.springframework.jdbc.core.namedparam.MapSqlParameterSource;
import org.springframework.jdbc.core.simple.SimpleJdbcInsert;

import javax.sql.DataSource;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.Optional;

public class JdbcTemplateMemberRepository implements MemberRepository{
    // JdbcTemplate을 먼저 받음
    private final JdbcTemplate jdbcTemplate;

    // Injection 하는 작업 datasource를 넣어줌, 이전에 생성자와는 살짝 다름
//    @Autowired // 생성자가 딱 하나 있다면 Autowired를 생략할 수 있음
    public JdbcTemplateMemberRepository(DataSource dataSource){
        jdbcTemplate = new JdbcTemplate(dataSource);
    }

    @Override
    public Member save(Member member) {
        // member 테이블에 대해서 id에 대한 key를 통해서 받아옴
        SimpleJdbcInsert jdbcInsert = new SimpleJdbcInsert(jdbcTemplate);
        jdbcInsert.withTableName("member").usingGeneratedKeyColumns("id");

        // 그렇게 해서 insert문을 만듬
        Map<String, Object> parameters = new HashMap<>();
        parameters.put("name", member.getName());

        // 이 부분에 대해서 편리하게 활용을 함
        Number key = jdbcInsert.executeAndReturnKey(new MapSqlParameterSource(parameters));
        member.setId(key.longValue());

        return member;
    }

    @Override
    public Optional<Member> findById(Long id) {
        // query를 통해서 id를 조회하는 부분, List로 넘어옴, 그래서 Optional로 반환을 함
        List<Member> result = jdbcTemplate.query("select * from member where id = ?", memberRowMapper());
        return result.stream().findAny();
    }

    @Override
    public Optional<Member> findByName(String name) {
        // query를 통해 name을 조회함
        List<Member> result = jdbcTemplate.query("select * from member where name = ?", memberRowMapper());
        return result.stream().findAny();
    }

    @Override
    public List<Member> findAll() {
        // 전체 조회함
        return jdbcTemplate.query("select * from member", memberRowMapper());
    }

    // findById에서 결과를 받기위해서 Mapping을 해줘야함
    // 그러면 결과로 넘어간 뒤 거기서 테이블에 있는 값을 가져옴
    private RowMapper<Member> memberRowMapper() {
        return (rs, rowNum) -> {
            Member member = new Member();
            member.setId(rs.getLong("id"));
            member.setName(rs.getString("name"));
            return member;
        };
    }
}
```

- 매우 단순해졌는데 jdbctemplate을 통해서 쿼리문을 날리고 콜백을 활용해서 그에 대한 결과를 받아오는 것임
- 그리고 추가적으로 configuration도 수정을 해주면 됨

```java
package hello.helloworld;

import hello.helloworld.repository.JdbcMemberRepository;
import hello.helloworld.repository.JdbcTemplateMemberRepository;
import hello.helloworld.repository.MemberRepository;
import hello.helloworld.repository.MemoryMemberRepository;
import hello.helloworld.service.MemberService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import javax.sql.DataSource;

@Configuration // 스프링이 configuration 먼저 읽음
public class SpringConfig {

    // Jdbc에 연결해주기 위한 DataSource를 받아줌
    private DataSource dataSource;

    @Autowired
    public SpringConfig(DataSource dataSource){
        this.dataSource = dataSource;
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
        return new JdbcTemplateMemberRepository(dataSource);
    }
}
```

- 그 다음 테스트 코드를 통해서 DB까지 연결해서 어떻게 되는지 확인할 수 있음
- 프로덕션이 커지면 테스트 코드가 매우 중요함
- 아직까지도 쿼리문을 활용하는 방식이 사용되는 것이긴 함