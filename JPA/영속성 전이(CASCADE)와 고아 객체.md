### 영속성 전이: CASCADE
![one](/img/JPA/Cascade/one.png)

- 부모 저장시 자식 저장하고 싶을 때 사용, 말 그대로 부모 호출 시 자식도 다 부르고 싶을 때 하는 것
![one](/img/JPA/Cascade/two.png)

- 코드로 보면 아래와 같음, 양방향으로 매핑한 것
```java
package hellojpa;

import javax.persistence.*;
import java.util.ArrayList;
import java.util.List;

@Entity
public class Parent {

    @Id @GeneratedValue
    private Long id;

    private String name;

    @OneToMany(mappedBy = "parent")
    private List<Child> childList = new ArrayList<>();

    // 연관관계 편의 메서드, 양방향 다 세팅을 해 줌
    public void addChild(Child child) {
        childList.add(child);
        child.setParent(this);
    }

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```
```java
package hellojpa;

import javax.persistence.*;

@Entity
public class Child {

    @Id
    @GeneratedValue
    private Long id;

    private String name;

    @ManyToOne
    @JoinColumn(name = "parent_id")
    private Parent parent;

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Parent getParent() {
        return parent;
    }

    public void setParent(Parent parent) {
        this.parent = parent;
    }
}
```

- 위와 같이 하면 기존에 추가를 할 때 아래와 같이 씀, 근데 여기서 parent만 persist하면 자동으로 child를 persist 해주고 싶을 때 CASCADE를 사용함
```java
Child child1 = new Child();
Child child2 = new Child();

Parent parent = new Parent();
parent.addChild(child1);
parent.addChild(child2);

em.persist(parent);
em.persist(child1);
em.persist(child2);
```

- 아래와 같이 CASCADE 설정을 할 수 있음, 그럼 parent만 넣은 것으로 child도 들어갈 수 있음
```java
package hellojpa;

import javax.persistence.*;
import java.util.ArrayList;
import java.util.List;

@Entity
public class Parent {

    @Id @GeneratedValue
    private Long id;

    private String name;

    @OneToMany(mappedBy = "parent", cascade = CascadeType.ALL) // cascade를 통해서 child 역시 parent만 persist 했을 때 적용됨
    private List<Child> childList = new ArrayList<>();

    // 연관관계 편의 메서드, 양방향 다 세팅을 해 줌
    public void addChild(Child child) {
        childList.add(child);
        child.setParent(this);
    }

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```
![one](/img/JPA/Cascade/three.png)

### CASCADE의 종류
![one](/img/JPA/Cascade/four.png)

### 고아 객체
![one](/img/JPA/Cascade/five.png)

- 연관관계가 끊어져서 삭제를 함
- 주의점
![one](/img/JPA/Cascade/six.png)

### 영속성 전이 + 고아객체, 생명주기
![one](/img/JPA/Cascade/seven.png)

- child 생명주기를 parent가 관리를 하는 것임, DDD에 Aggregate Root 개념을 구현할 때 유용함