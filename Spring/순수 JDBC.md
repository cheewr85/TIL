- 애플리케이션과 DB를 연결해서 insert 하면 DB에 저장을 할 수 있게끔 할 것임
- 지금 이 순수 JDBC는 예전에 활용한 방식임
- 먼저 build.gradle에 아래 코드를 추가함, 라이브러리 추가

```java
implementation 'org.springframework.boot:spring-boot-starter-jdbc'
runtimeOnly 'com.h2database:h2'
```

- 그 다음 추가적으로 application.properties에 대해서 추가를 해줘야함, 스프링 부트 데이터베이스에 연결을 추가하는 것임

```java
spring.datasource.url=jdbc:h2:tcp://localhost/~/test
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.username=sa
```

- 이 작업을 하면 데이터베이스에 접근하는 작업은 완료된 것임, 스프링을 실행시키면 자동으로 DB에 연결되는 것임
- 그 다음 여기서 이전에 기능만을 정의한 MemberRepository를 일단 Memory로 활용을 했기 때문에 Memory에 대한 Repository로 사용을 했지만 이제 JDBC로 H2 데이터베이스를 연결해서 하는것이 명확해졌기 때문에 이에 대해서 새로운 클래스를 추가하면 됨

```java
package hello.helloworld.repository;

import hello.helloworld.domain.Member;

import java.util.List;
import java.util.Optional;

public class JdbcMemberRepository implements MemberRepository{
    @Override
    public Member save(Member member) {
        return null;
    }

    @Override
    public Optional<Member> findById(Long id) {
        return Optional.empty();
    }

    @Override
    public Optional<Member> findByName(String name) {
        return Optional.empty();
    }

    @Override
    public List<Member> findAll() {
        return null;
    }
}
```

- 이제 여기서 하나씩 구현을 해나가면 됨
- 러프하게 save 하는 코드를 짜면 아래와 같음

```java
@Override
    public Member save(Member member) {
        // DB에 저장하기 위한 Query를 짬
        String sql = "insert into member(name) values(?)";
        // DB의 커넥션을 가지고 옴
        Connection connection = dataSource.getConnection();
        // 그 다음 커넥션 연결후 쿼리문 문장 작성함
        PreparedStatement pstmt = connection.prepareStatement(sql);
        // 그 다음 넣어줄 값을 처리
        pstmt.setString(1, member.getName());
        // DB에 쿼리를 날림
        pstmt.executeUpdate();
        return null;
    }
```

- 하지만 실질적으로 Memory 부분을 참조하면 sequence 값도 넣어줘야하고 확인을 해야하므로 이런 부분에 대해서 처리를 더 해줘야 함
- 실제 코드는 아래와 같음

```java
package hello.helloworld.repository;

import hello.helloworld.domain.Member;
import org.springframework.jdbc.datasource.DataSourceUtils;

import javax.sql.DataSource;
import java.sql.*;
import java.util.ArrayList;
import java.util.List;
import java.util.Optional;

public class JdbcMemberRepository implements MemberRepository {

    // DB에 붙기 위해서 dataSource가 필요함
    private final DataSource dataSource;

    // 추후에 Spring에서 주입받아야함, 이전에 properties에 설정을 해둬서 스프링이 이미 데이터베이스에 접속 정보를 만들어뒀음
    // 그 접속 정보를 나중에 스프링에서 주입을 함
    public JdbcMemberRepository(DataSource dataSource) {
        this.dataSource = dataSource;
    }

    @Override
    public Member save(Member member) {
        // DB에 저장하기 위한 Query를 짬
        String sql = "insert into member(name) values(?)";

        Connection conn = null;
        PreparedStatement pstmt = null;
        ResultSet rs = null; // 결과를 받음음

       try {
           // connection을 먼저 받고 sql을 넣음
            conn = getConnection();
            pstmt = conn.prepareStatement(sql,
                    Statement.RETURN_GENERATED_KEYS); // insert를 위해서 씀

            pstmt.setString(1, member.getName()); // 1은 파라미터로 ?와 매칭되어 넣음

            pstmt.executeUpdate(); // 실제 업데이트를 함 DB에 SQL문 날라감
            rs = pstmt.getGeneratedKeys(); // DB가 생성한 id 1,2.. 자동으로 들어간 값을 받아옴

            if (rs.next()) { //값이 있으면 꺼내게 함
                member.setId(rs.getLong(1));

            } else { // 실패하면 조회하게 함
                throw new SQLException("id 조회 실패");
            }
            return member;
        } catch (Exception e) {
            throw new IllegalStateException(e);
        } finally {
           // 자원을 풀어줘야함, 그렇지 않으면 쌓여서 오류가 남
            close(conn, pstmt, rs);
        }

    }

    @Override
    public Optional<Member> findById(Long id) {
        // 조회를 위해서 쿼리를 날림
        String sql = "select * from member where id = ?";

        Connection conn = null;
        PreparedStatement pstmt = null;
        ResultSet rs = null;

        try {
            // conn 날리고 세팅을 하고
            conn = getConnection();
            pstmt = conn.prepareStatement(sql);
            pstmt.setLong(1, id);
            // 쿼리를 해서 result를 본 다음
            rs = pstmt.executeQuery();

            if (rs.next()) {
                // 멤버 객체를 생성해서 쭉 만들어주면 됨
                Member member = new Member();
                member.setId(rs.getLong("id"));
                member.setName(rs.getString("name"));

                return Optional.of(member);

            } else {

                return Optional.empty();

            }

        } catch (Exception e) {

            throw new IllegalStateException(e);

        } finally {

            close(conn, pstmt, rs);

        }

    }

    @Override
    public List<Member> findAll() {
        // sql로 조회시작
        String sql = "select * from member";
        Connection conn = null;
        PreparedStatement pstmt = null;
        ResultSet rs = null;

        try {
            // 조회한걸 바탕으로 이걸 조회한 멤버 모두를 쭉 담음
            conn = getConnection();
            pstmt = conn.prepareStatement(sql);
            rs = pstmt.executeQuery();
            List<Member> members = new ArrayList<>();

            while (rs.next()) {
                Member member = new Member();
                member.setId(rs.getLong("id"));
                member.setName(rs.getString("name"));
                members.add(member);

            }
            return members;

        } catch (Exception e) {

            throw new IllegalStateException(e);

        } finally {

            close(conn, pstmt, rs);

        }

    }

    @Override
    public Optional<Member> findByName(String name) {
        // name을 찾고 받은 다음에 쭉 넘겨서
        String sql = "select * from member where name = ?";
        Connection conn = null;
        PreparedStatement pstmt = null;
        ResultSet rs = null;

        try {
            conn = getConnection();
            pstmt = conn.prepareStatement(sql);
            pstmt.setString(1, name);
            rs = pstmt.executeQuery();

            if (rs.next()) {
                Member member = new Member();
                member.setId(rs.getLong("id"));
                member.setName(rs.getString("name"));

                return Optional.of(member);

            }

            return Optional.empty();

        } catch (Exception e) {

            throw new IllegalStateException(e);

        } finally {

            close(conn, pstmt, rs);

        }

    }

    private Connection getConnection() {
        // datasourceutils를 통해서 connection을 얻음, spring 프레임워크 쓰면 그럼
        return DataSourceUtils.getConnection(dataSource);

    }

    private void close(Connection conn, PreparedStatement pstmt, ResultSet rs) {
        try {
            // rs를 닫아주고
            if (rs != null) {
                rs.close();
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        try {
            // preparedstatement 확인하고
            if (pstmt != null) {
                pstmt.close();
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        try {
            // conn 닫아주고
            if (conn != null) {
                close(conn);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private void close(Connection conn) throws SQLException {
        // 닫을 때도 datasourceutils를 통해서 활용함
        DataSourceUtils.releaseConnection(conn, dataSource);
    }
}
```

- 이런식으로 DB에 접근해서 어떻게 처리할 지 정했다면 그 다음엔 configuration을 해줘야함
- 이전에 수동으로 Bean에 올린 작업에 대해서 Jdbc로 바꿔주면 됨

```java
package hello.helloworld;

import hello.helloworld.repository.JdbcMemberRepository;
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
        return new JdbcMemberRepository(dataSource);
    }
}
```

- 위처럼 설정을 다시 해주면 됨 Configuration을 정상적으로 처리했다면 이전에 했던 spring, spring2가 회원 목록에 아래와 같이 존재함

![one](/img/Spring/H2/four.png)

- 등록을 해도 이 부분이 DB에 저장이 됨
- 아래와 같은 구조가 되는 것임

![one](/img/Spring/H2/five.png)

- 하지만 Configuration을 손 봄으로써 아래와 같이 구조가 바뀐 것임

![one](/img/Spring/H2/six.png)

- 이렇게 되면 구현체만 바뀌어서 돌아가게 됨, 이를 개방-폐쇄 원칙이라고 함

![one](/img/Spring/H2/seven.png)

