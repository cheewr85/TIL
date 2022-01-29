### @MappedSuperClass
![one](/img/JPA/Mapped/one.png)

- 단순하게 객체 입장에서 id & name이 계속 나옴, 공통 속성만 상속하고 싶다면 할 때 DB가 다른데 공통 속성만 상속받아 사용하고 싶을 때 쓰는 것
- 만약 중복 정보 시간과 작성자를 무조건 담아야 한다고 할 때 아래와 같이 추가된다고 함, 모든 테이블에 다 들어간다고 가정하면
```java
private String createdBy;
private LocalDateTime createdDate;
private String lastModifiedBy;
private LocalDateTime lastModifiedDate;
```

- 이때 속성만 상속 받기 위해서 위의 속성만 뽑아서 클래스를 만듬 BaseEntity 상속받음
- 단 여기서 BaseEntity에서 `@MappedSuperClass` 필수로 들어가야함
```java
package hellojpa;

import java.time.LocalDateTime;

@MappedSuperClass
public class BaseEntity {

    private String createdBy;
    private LocalDateTime createdDate;
    private String lastModifiedBy;
    private LocalDateTime lastModifiedDate;

    public String getCreatedBy() {
        return createdBy;
    }

    public void setCreatedBy(String createdBy) {
        this.createdBy = createdBy;
    }

    public LocalDateTime getCreatedDate() {
        return createdDate;
    }

    public void setCreatedDate(LocalDateTime createdDate) {
        this.createdDate = createdDate;
    }

    public String getLastModifiedBy() {
        return lastModifiedBy;
    }

    public void setLastModifiedBy(String lastModifiedBy) {
        this.lastModifiedBy = lastModifiedBy;
    }

    public LocalDateTime getLastModifiedDate() {
        return lastModifiedDate;
    }

    public void setLastModifiedDate(LocalDateTime lastModifiedDate) {
        this.lastModifiedDate = lastModifiedDate;
    }
}
```
```java
package hellojpa;

import javax.persistence.*;
import java.util.ArrayList;
import java.util.Date;
import java.util.List;

@Entity // JPA가 로딩될 때 JPA 사용하는 것임을 인식함
public class Member extends BaseEntity{

    @Id @GeneratedValue
    @Column(name = "MEMBER_ID")
    private Long id;

    @Column(name = "USERNAME")
    private String username;

//    @Column(name = "TEAM_ID")
//    private Long teamId;

    @ManyToOne // 멤버가 N이고 Team은 1인 관계이므로
    // 해당 어노테이션은 JPA에게 관계를 알려주고 DB 관점에서도 맵핑이되는거니깐 처리하기 위해서 설정해줘야함
    @JoinColumn(name = "TEAM_ID") // Team과 Member 테이블에서 Foreign Key와 매핑해야 하므로 해당 Column으로 Join 하는 것
    private Team team;

    @OneToOne // 일대일 관계 설정
    @JoinColumn(name = "LOCKER_ID")
    private Locker locker;

    @ManyToMany // 다대다 관계 설정
    @JoinTable(name = "MEMBER_PRODUCT")
    private List<Product> products = new ArrayList<>();

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public Team getTeam() {
        return team;
    }

    public void setTeam(Team team) {
        this.team = team;
    }

    public void changeTeam(Team team) {
        this.team = team;
        team.getMembers().add(this); // Member(this) 나 자신을 추가
    }
}
```

![one](/img/JPA/Mapped/two.png)
![one](/img/JPA/Mapped/three.png)

