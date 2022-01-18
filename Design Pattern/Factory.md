### Factory 패턴
- Template 패턴의 인스턴스 생성의 장면에 적용한 것이 Factory 패턴임
- Factory 패턴에서는 인스턴스를 만드는 방법을 상위 클래스 측에서 결정하지만 구체적인 클래스 이름까지는 결정하지 않음, 구체적인 내용은 모두 하위 클래스 측에서 수행함
- 인스턴스 생성을 위한 골격(framework)과 실제의 인스턴스 생성의 클래스를 분리해서 생각할 수 있음

![one](/img/DesignPattern/Factory/one.png)

- Product 클래스와 Factory 클래스는 framework라는 패키지에 속해 있음, 이 두 개의 클래스가 인스턴스 생성을 위한 골격(framework)역할을 함
- IDCard 클래스와 IDCardFactory 클래스는 구체적인 내용을 구현하며 idcard라는 패키지에 속해있음
- 인스턴스 생성의 framework측(Framework 패키지)
- 구체적인 내용을 구현하고 있는 측(idcard 패키지)
- framework
    - Product
        - 추상 메소드 use만 정의되어 있는 추상 클래스
    - Factory
        - 메소드 create을 구현하고 있는 추상 클래스
- idcard
    - IDCard
        - 메소드 use를 구현하고 있는 클래스
    - IDCardFactory
        - 메소드 createProduct, registerProduct를 구현하고 있는 클래스
- Anonymous
    - Main
        - 동작 테스트용 클래스

### Product
```java
package framework;

public abstract class Product {
		public abstract void use();
}
```
- framework 패키지의 Product 클래스(제품을 표현한 클래스), 추상 메소드 use만이 선언되어 있음
- 구체적인 use의 구현은 모두 Product 하위 클래스에게 맡기고 있음
- 이 framework에서는 제품이란 무엇이든 use할 수 있는 것으로 규정함

### Factory
```java
package framework;

public abstract class Factory {
		public final Product create(String owner) {
				Product p = createProduct(owner);
				registerProduct(p);
				return p;
		}
		protected abstract Product createProduct(String owner);
		protected abstract void registerProduct(Product product);
}
```
- Factory 클래스는 Template 패턴을 사용하고 있음
- 추상 메소드 createProduct는 제품을 만들고 만든 제품을 추상 메소드 registerProduct에 등록함
- 제품을 만들고 등록하는 구현은 하위 클래스에서 수행함
- framework 패키지는 create 메소드에서 Product의 인스턴스를 생성하는 것으로 규정, 그리고 create 메소드는 createProduct에서 제품을 만들어서 registerProduct에서 등록한다는 순서로 구현됨
- 구체적인 내용은 Factory 패턴을 적용한 프로그램에 따라 다름, Factory 패턴에서 인스턴스 생성할 때 Template 패턴을 사용함

### IDCard
```java
package idcard;
import framework.*;

public class IDCard extends Product {
		private String owner;
		IDCard(String owner) {
				System.out.println(owner + "의 카드를 만듭니다.");
				this.owner = owner;
		}
		public void use() {
				System.out.println(owner + "의 카드를 사용합니다.");
		}
		public String getOwner() {
				return owner;
		}
}
```
- IDCard 클래스를 제품 product 하위 클래스로 정의함

### IDCardFactory
```java
package idcard;
import framework.*;
import java.util.*;

public class IDCardFactory extends Factory {
		private List owners = new ArrayList();
		protected Product createProduct(String owner) {
				return new IDCard(owner);
		}
		protected void registerProduct(Product product) {
				owners.add(((IDCard)product).getOwner());
		}
		public List getOwners() {
				return owners;
		}
}
```
- createProduct와 registerProduct의 두 가지 메소드를 구현함
- createProduct에서는 IDCard의 인스턴스를 생성해서 제품을 만드는 일을 실현하고 있음
- registerProduct에서는 IDCard의 owner(소유자)를 owners 필드에 추가해서 등록이라는 기능을 실현하고 있음

### Main
```java
import framework.*;
import idcard.*;

public class Main {
		public static void main(String[] args) {
				Factory factory = new IDCardFactory();
				Product card1 = factory.create("홍길동");
				Product card2 = factory.create("이순신");
				Product card3 = factory.create("강감찬");
				card1.use();
				card2.use();
				card3.use();
		}
}
```
- Factory를 생성할 때 IDCardFactory로 인스턴스 생성함, 그러면 createProduct와 registerProduct등의 구현한 부분 사용할 수 있음
- card를 각각 factory 즉 IDCardFactory 인스턴스를 가지고 create를 함, 그러면 Factory 클래스에 있는대로 createProduct와 함께 registerProduct를 하고 p를 return함
- 여기서 각각의 매개변수로 owner를 넘겼고 그 세부적인 과정은 IDCardFactory 클래스에 구현한대로 생성자를 IDCard로 만들고 owners 필드에 저장함, 이때 IDCard에서 생성시 `의 카드를 만듭니다`가 함께 출력됨
- 그리고 card1.use를 하게 되면 Product의 use 메소드를 쓰는것인데 이 부분 역시 IDCard에 설정되어 있음 만드는 과정에서 IDCard 인스턴스로 생성되어져서 등록된 것이므로 use 사용시 IDCard 클래스에서 구현되어 있는 내용 `의 카드를 사용합니다`가 함께 출력됨

### 패턴의 등장인물
![one](/img/DesignPattern/Factory/two.png)

- 상위 클래스(추상적인 골격, framework)측에 있는 Creator 역할과 Product 역할의 관계가 하위 클래스(구체적인 내용, idcard)측에 있는 ConcreteCreator 역할과 ConcreteProduct 역할의 관계와 병행하고 있음
- Product(제품)의 역할
    - framework 쪽에 포함되어 있음, 인스턴스가 가져야 할 인터페이스(API)를 결정하는 것은 추상 클래스임
    - 구체적인 내용은 하위 클래스의 ConcreteProduct 역할이 결정함
    - 예제 프로그램에서 Product 클래스가 이 역할을 함
- Creator(작성자)의 역할
    - Product 역할을 생성하는 추상 클래스는 framework 쪽에 가까움, 구체적인 내용은 위 클래스의 ConcreteCreator 역할이 결정함
    - 예제 프로그램에서는 Factory 클래스가 이 역할을 수행함
    - Creator 역할이 가지고 있는 정보는 Product 역할과 인스턴스 생성의 메소드를 호출하면 Product가 생성된다는 것뿐임
    - 예제 프로그램에서는 createProduct 메소드가 인스턴스 생성을 위한 메소드가 됨
    - new를 사용해서 실제의 인스턴스를 생성하는 대신에, 인스턴스 생성을 위한 메소드를 호출해서 구체적인 클래스 이름에 의한 속박에서 상위 클래스를 자유롭게 만듬
- ConcreteProduct(구체적인 제품)의 역할
    - 구체적인 제품을 결정하며, idcard쪽에 해당함, 예제 프로그램에서 IDCard 클래스가 이 역할을 함
- ConcreteCreator(구체적인 작성자)의 역할
    - 구체적인 제품을 만드는 클래스를 결정하며, idcard 쪽에 해당함, 예제 프로그램에서 IDCardFactory가 이 역할을 수행함

## 사고력 키우기

### framework와 구체적인 내용
- 추상적인 골격과 구체적인 내용 두 가지 측면에서 framework 패키지와 idcard 패키로 나눔
- 여기서 동일한 framework를 사용해서 전혀 다른 제품과 공장을 만든다고 할 때 만약 TV의 클래스와 TV공장 Television, TelevisionFactory를 만든다면 framework 패키지를 import한 별도의 Television 패키지를 만듬
- 여기서 framework 패키지의 내용을 수정하지 않아도 전혀 다른 제품과 공장을 만들 수 있음, framework 패키지의 내용을 수정할 필요가 없음
- 즉 위의 예시에서 idcard 역시 framework 패키지의 내용을 수정할 필요가 없는데 이는, framework 패키지는 idcard 패키지에 의존하고 있지 않다고 함

### 인스턴스 생성 - 메소드의 구현 방법
- 예제 프로그램에서 Factory 클래스의 createProduct 메소드는 추상 메소드이며, 하위 클래스에서 구현을 함
- createProduct 메소드의 기술 방법은 다음과 같이 세 가지로 생각할 수 있음
    - 추상 메소드로 함
        - 추상 메소드로 하면 하위 클래스는 반드시 이 메소드를 구현해야함, 구현되어 있지 않으면 컴파일 할 때 검출됨
        - 예제에선 아래와 같이 했음
        
        ```java
        abstract class Factory {
        		public abstract Product createProduct(String name);
        		...
        }
        ```
        
    - 디폴트의 구현을 준비해 둔다
        - 디폴트의 구현을 준비해 두고 하위 클래스에서 구현하지 않았을 때 사용하면 됨
        
        ```java
        class Factory {
        		public Product createProduct(String name) {
        				return new Product(name);
        		}
        		...
        }
        ```
        
        - 단, 이 경우에는 Product 클래스에 대해서 직접 new를 이용하고 있으므로 Product 클래스를 추상 클래스로 둘 수 없음
    - 에러를 이용함
        - 디폴트의 구현 내용을 에러로 처리해 두면 하위 클래스에서 구현하지 않았을 경우에는 실행할 때 에러가 발생함(에러가 발생해서 구현되고 있지 않은 것을 알려줌, 여기서 ㅓ예외는 별도로 작성되어 있다고 가정)
        
        ```java
        class Factory {
        		public Product createProduct(String name) {
        				throw new FactoryMethodRuntimeException();
        		}
        		...
        }
        ```
        

### 패턴 이용과 개발자 간의 의사소통
- 상위 클래스에서 동작의 골격을 이해하고, 거기에서 사용되고 있는 추상 메소드가 무엇인지를 확인하고, 또한 그 추상 메소드를 실제로 구현하고 있는 클래스의 소스 코드를 살펴볼 필요가 있음

### 안드로이드 이용
- 직접적인 사용 예제보다도 위에서 활용한 기능 그대로 안드로이드에서도 응용함
- 예를 들어서 책 이름을 입력받고 작가의 이름을 리턴하는 방식에 있어서 Factory 패턴을 사용해서 이름을 리턴하는 식으로 등에 활용가능