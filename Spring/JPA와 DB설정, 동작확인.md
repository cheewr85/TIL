### JPA와 DB 설정, 동작확인

- 기존의 [application.properties](http://application.properties) 대신 application.yml로 파일을 만듬, 이는 properties를 쓰느냐 yml을 쓰느냐 선택의 차이임
- 그리고 DB 설정 등 연결을 위한 세팅을 해야함, 이때 강의와는 상이하게 MVCC=TRUE를 넣어주지 않아도 됨
- hibernate : ddl-auto는 자동으로 테이블을 만들고 drop하게 함, 자동처리
- jpa 설정 properties 등의 내용에 대한 것은 SpringBoot 공식 문서상 Document를 통해서 알 수 있음(옵션들)
- hibernate에서 SQL의 모든 것이 debug로 로그를 통해 알 수 있음

```java
spring:
  datasource:
    url: jdbc:h2:tcp://localhost/~/jpashop
    username: sa
    password:
    driver-class-name: org.h2.Driver

  jpa:
    hibernate:
      ddl-auto: create
    properties:
      hibernate:
        #        show_sql: true
        format_sql: true

logging.level:
  org.hibernate.SQL: debug
#  org.hibernate.type: trace
```

- 그 다음 DB 테스트를 위해서 Member를 직접 만듬 JPA 어느정도 안다는 가정하에 만듬
- 각 값에 대한 Member와 해당 클래스 만듬

```java
package jpabook.jpashop;

import lombok.Getter;
import lombok.Setter;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;

@Entity
@Getter @Setter
public class Member {

    @Id @GeneratedValue
    private Long id;
    private String username;

}
```

- 그 다음 Repository 생성, Repository는 Entity를 찾아주는 것 Dao와 비슷한 것
- 알아서 manager를 생성하고 설정됨

```java
package jpabook.jpashop;

import org.springframework.stereotype.Repository;

import javax.persistence.EntityManager;
import javax.persistence.PersistenceContext;

@Repository
public class MemberRepository {

    @PersistenceContext
    private EntityManager em;

    public Long save(Member member) {
        em.persist(member);
        return member.getId(); // 아이디만 우선적으로 조회
    }

    public Member find(Long id) {
        return em.find(Member.class, id); // Member 조회
    }
}
```

- 그 다음 Test코드를 만듬, 그리고 실행시켜봄

```java
package jpabook.jpashop;

import org.assertj.core.api.Assertions;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.transaction.annotation.Transactional;

import static org.junit.Assert.*;

@RunWith(SpringRunner.class)
@SpringBootTest
public class MemberRepositoryTest {

    @Autowired MemberRepository memberRepository; // 인젝션을 받음

    @Test
    @Transactional // Transaction 설정도 해줘야함
    public void testMember() throws Exception {
        //given, 멤버 잘 저장됐는지 확인
        Member member = new Member();
        member.setUsername("memberA");

        //when, 저장된 아이디를 뽑음 위에서 set을 했으니깐
        Long savedId = memberRepository.save(member);
        Member findMember = memberRepository.find(savedId);

        //then, 잘 저장됐는지 검증을 함
        Assertions.assertThat(findMember.getId()).isEqualTo(member.getId());
        Assertions.assertThat(findMember.getUsername()).isEqualTo(member.getUsername());

    }

}
```

- 그리고 H2 데이터베이스와 연결을 해보면 MEMBER 테이블이 있는 것을 알 수 있음

![one](/img/Spring/Set/one.png)

- 데이터가 비어 있음을 알 수 있는데, 이는 Test 코드 실행 후 완료가 되면 Transactional 어노테이션으로 인해서 롤백을 해버리기 때문에 그럼, 여기서 Rollback(false)하고 하면 데이터가 롤백이 되지않고 들어옴

```java
package jpabook.jpashop;

import org.assertj.core.api.Assertions;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.annotation.Rollback;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.transaction.annotation.Transactional;

import static org.junit.Assert.*;

@RunWith(SpringRunner.class)
@SpringBootTest
public class MemberRepositoryTest {

    @Autowired MemberRepository memberRepository; // 인젝션을 받음

    @Test
    @Transactional // Transaction 설정도 해줘야함
    @Rollback(false) // 롤백을 하지 않고 데이터를 보존함
    public void testMember() throws Exception {
        //given, 멤버 잘 저장됐는지 확인
        Member member = new Member();
        member.setUsername("memberA");

        //when, 저장된 아이디를 뽑음 위에서 set을 했으니깐
        Long savedId = memberRepository.save(member);
        Member findMember = memberRepository.find(savedId);

        //then, 잘 저장됐는지 검증을 함
        Assertions.assertThat(findMember.getId()).isEqualTo(member.getId());
        Assertions.assertThat(findMember.getUsername()).isEqualTo(member.getUsername());

    }

}
```

- 여기서 findMember와 member자체를 비교해보면 true가 나옴을 알 수 있음, 영속성에서 같은 엔티티로 인식을 하면 같은 식별자로써 인식을 함으로써 같은 값으로 볼 수 있음
- gradlew 상, jar상 cmd 상에서 실행을 해서 확인을 할 수 있음
- 로깅을 확인하기 위해서 아래와 같이 yml에 추가해서 확인할 수 있음
- *`org.hibernate.type: trace`*
- 혹은 외부 라이브러리를 써서 확인할 수 있음
- 해당 링크중 P6Spy를 사용할 수 있음 https://github.com/gavlyukovskiy/spring-boot-data-source-decorator
- 그리고 이 코드 추가해서 라이브러리 추가할 수 있음
- `implementation "com.github.gavlyukovskiy:p6spy-spring-boot-starter:1.8.0"`
- 그리고 테스트 실행시 결과의 출력정보가 그대로 나옴, 아래와 같이

![one](/img/Spring/Set/two.png)

- 개발단계에서는 괜찮지만 배포하는 단계에서는 고려를 해야함

### 부연설명

- lombok 사용하여서 Getter, Setter를 직접 자바 코드로 함수를 작성하지 않고 어노테이션 처리로 한 번에 처리를 해 줌
- Entity 어노테이션의 경우, jpa.hibernate.ddl-auto를 create 설정을 하게 되면 이 어노테이션 자체만으로 데이터베이스의 테이블을 자동으로 생성을 할 수 있게함, 이는 이 어노테이션을 통해서 Repository내에서 EntityManager가 Member에 해당하는 테이블을 만들어주는 것임
- Member에서 Id 어노테이션은 데이터베이스 테이블의 기본값인 Primary Key를 생성하게 함
- GeneratedValue를 통해서 앞서 정의한 Long id 값이 PK가 되면서 자동 증가값이 됨으로써 알아서 데이터베이스 테이블의 PK설정이 완료되는 것임
- 여기서 Entity 어노테이션으로 데이터베이스 테이블을 만들고 Getter,Setter도 만들었으므로 그 값을 설정 및 불러와서 처리를 할 수 있음 여기서 직접적으로 이를 DB에 저장하고 관리하고 데이터베이스에 접근하기 위한 레포지토리가 필요하기 때문에 Repository 어노테이션을 붙인것뿐 아니라 EntityManager를 통해서 앞서 Entity 어노테이션으로 정의한 데이터베이스 테이블을 처리할 수 있음, 구조는 우선 아래와 같음
- 여기서 하나 더 짚고 넘어가야 할 부분은 Entity Manager의 경우 PersistenceContext를 통해서 빈에 등록할 수 있음

![one](/img/Spring/Set/three.png)

- 아래와 같은 구조로 생겨서 빈을 등록한다고 봐도 무방함, 메소드 안에서 EntityManage em이 사용하는 메소드명을 보면 아래와 같이 작용한다고 볼 수 있음

![one](/img/Spring/Set/four.png)

- 이 빈을 등록한다는 것은 컨테이너에 담는다는것인데 아래와 같이 단순히 template과 같은것 외에도 앞서 쓴 부분들이 담기는 것임

![one](/img/Spring/Set/five.png)

- 그래서 AutoWired 즉, 자동으로 Test 코드 실행시 MemberRepository를 등록해서 사용하는 것이고, 거기에 있는 save, find를 통해서 DB에 접근해서 테스트를 할 수 있는 것임
- RunWith은 JUnit4의 테스트를 위한 SpringBootTest는 스프링부트의 통합 테스트 Test는 테스트를 위한 메소드를 의미함
- Transactional 어노테이션의 경우 DB에 접근하는 모든 객체 또는 메소드 위에  쓰이는 것으로 테스트 성공시 DB에 저장하고 실패시 rollback을 함 default가 테스트 완료 후 롤백인데 이는 DB에 영향을 주지 않으려고 그러는 것인데 여기서 Rollback(false)를 하면 롤백을 하지 않고 DB에 남음
- 각각의 메소드는 위의 EntityManager에서 보이는 그림과 같이 그런 과정을 위해서 쓰는 메소드들임