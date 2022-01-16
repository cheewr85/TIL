- 아래와 같이 Book이라는 클래스가 있고 해당 값을 find 한다고 할 때 Transaction에서 set을 하고 commit을 해버리면 변경부분에 대해서 JPA가 자동으로 찾아서 업데이트 쿼리를 적용해 자동으로 변경사항을 반영을 함 ⇒ 더티 체킹(변경 감지)
- 이 매커니즘으로 기본적으로 JPA의 엔티티를 바꿀 수 있음

```java
package jpabook.jpashop.service;

import jpabook.jpashop.domain.Member;
import jpabook.jpashop.domain.item.Book;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

import javax.persistence.EntityManager;

import static org.junit.Assert.assertEquals;

@RunWith(SpringRunner.class)
@SpringBootTest
public class ItemUpdateTest {

    @Autowired
    EntityManager em;

    @Test
    public void updateTest() throws Exception {
        Book book = em.find(Book.class, 1L);

        // Tx
        book.setName("asdfers");

        // 변경감지 == dirty checking
        // Tx commit
    }
}
```

- 이 예시는 Order에서 주문 상태에 대해서 set만 해주고 JPA에 별도의 DB에 바꾸라고 하지 않았는데 한 것이 동일하게 쓰임
- 이런식으로 CANCEL로 바꿨는데 이렇게 값을 바꿔놓으면 JPA가 알아서 값이 바뀐걸 보고 Transaction commit 시점에 바뀐 것을 찾아가지고 DB에 업데이트 문을 날리고 Transaction commit을 함, flush 할 때 일어나는 것
- 데이터 변경시에 가장 기본 매커니즘임

```java
//==비즈니스 로직==//
    /**
     * 주문 취소
     */
    // 취소하면서 재고도 변경되는 그런 로직임
    public void cancel() {
        // 배송이 이미 되어 끝나버렸다면 취소가 불가능함, 해당 상태의 예외처리를 함
        if(delivery.getStatus() == DeliveryStatus.COMP) {
            throw new IllegalStateException("이미 배송완료된 상품은 취소가 불가능합니다.");
        }
        // 위의 예외처리를 빠져나왔다면 취소가 가능하므로 상태를 바꿔주면 됨
        this.setStatus(OrderStatus.CANCEL);
        // 루프를 돌면서 재고를 건드릴 것임(취소한만큼 다시 수량을 추가해줘야 하므로)
        for(OrderItem orderItem : orderItems) {
            // orderItem에도 각각 다 cancel을 해줘야하므로 반복문으로 체크를 함
            orderItem.cancel();
        }
    }
```

- 하지만 문제가 되는 것은 아래와 같은 경우임, 준영속 엔티티일 때

![one](/img/Spring/WebLayer/three.png)

- JPA 영속성 컨텍스트가 더 이상 관리하지 않는 엔티티를 말함
- 이는 아래와 같이 updateItem 부분이 해당함, 업데이트를 하면 BookForm을 통해서 데이터가 넘어옴, 그러면 Book을 생성하는데 객체는 새로운 객체가 맞는데 id가 세팅이 되어 있음
- 즉, 뭔가 JPA에 한 번 들어갔다가 나온 것을 의미함, DB에 갔다온 상태를 식별자가 정확하게 있는 것을 준영속 상태 객체라고 함
- 즉 위의 설명대로 더는 영속성 컨텍스트가 관리하지 않는 것임, 이미 DB에서 저장되고 불러온 상태이기 때문에, Book이 준영속 엔티티임

```java
// 수정하도록 맵핑함
    @PostMapping("items/{itemId}/edit")
    public String updateItem(@ModelAttribute("form") BookForm form) {

        Book book = new Book();
        book.setId(form.getId());
        book.setName(form.getName());
        book.setPrice(form.getPrice());
        book.setStockQuantity(form.getStockQuantity());
        book.setAuthor(form.getAuthor());
        book.setIsbn(form.getIsbn());

        itemService.saveItem(book);
        return "redirect:/items";
    }
```

- 문제는 이 준영속 엔티티는 JPA가 관리를 하지 않음, 영속상태는 변경감지와 모든걸 JPA가 보고 관리를 하는데 준영속은 그렇지 않음 즉, 업데이트가 일어나지 않는 것임
- 이런 준영속 상태는 아래와 같이 2가지 방법으로 수정을 할 수 있음

![one](/img/Spring/WebLayer/four.png)

- 첫 번째 변경 감지, dirty checking은 아래와 같이 할 수 있음
- 여기서 updateItem 로직에서 굳이 별도로 save 할 필요 없음, 이미 findItem으로 찾아온 것 자체가 영속상태임 그래서 값을 세팅한 다음에 끝내도 Transactional 어노테이션을 통해서 Transaction이 commit이 됨
- commit이 딱 되면 JPA는 flush를 날림, 영속성 컨텍스트 중 변경된 것이 뭔지 다 찾음
- 찾아서 바뀐 것에 대해서 바뀐 값을 찾아서 업데이트 쿼리를 DB에 날려서 침
- 이런식으로 변경 감지에 의해서 데이터를 변경할 수 있음

```java
package jpabook.jpashop.service;

import jpabook.jpashop.domain.item.Book;
import jpabook.jpashop.domain.item.Item;
import jpabook.jpashop.repository.ItemRepository;
import lombok.RequiredArgsConstructor;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

import java.util.List;

@Service
@Transactional(readOnly = true)
@RequiredArgsConstructor
public class ItemService {

    private final ItemRepository itemRepository;

    @Transactional // 상품 저장(쓰기이므로 Transactional 추가)
    public void saveItem(Item item) {
        itemRepository.save(item);
    }

    @Transactional // 변경 감지를 해서 업데이트 하기 위한 로직(준영속 컨텍스트에 대해)
    public void updateItem(Long itemId, Book param) {
        // 먼저 아이템을 찾음, Id기반으로 실제 영속상태 엔티티를 찾아옴
        Item findItem = itemRepository.findOne(itemId);
        // 그 다음 넘겨받음 Book param에서 값을 가져와 findItem에 set을 해주면 됨, 이런식으로 수정할 것 다 반영해줌
        findItem.setPrice(param.getPrice());
        findItem.setName(param.getName());
        findItem.setStockQuantity(param.getStockQuantity());
        // 수정을 다 한 후 마지막에 별도로 리포지토리 불러서 save나 아무것도 안해도 됨
    }

    // 상품 조회
    public List<Item> findItems() {
        return itemRepository.findAll();
    }

    // 상품 아이템 하나 조회
    public Item findOne(Long itemId) {
        return itemRepository.findOne(itemId);
    }
}
```

![one](/img/Spring/WebLayer/five.png)

- 이런 방식이 일반적으로 더 나은 방식임

![one](/img/Spring/WebLayer/six.png)
![one](/img/Spring/WebLayer/seven.png)

- 또 다른 한 가지 남은 방법은 병합(merge)을 사용하는 것임
- 병합은 준영속 상태의 엔티티를 영속 상태로 변경할 때 사용하는 기능임
- 이 부분은 코드로 보면 아래와 같이 save 상황에서 item 값이 있으면 merge를 하게 함
- 이 merge는 위에서 작성한 updateItem을 Transactional 어노테이션을 통해서 변경 감지 한 것과 똑같은 것임
- 즉, DB에서 item 식별자를 똑같이 찾고 그 다음 파리미터로 넣어놓은 객체를 찾아온 것의 값을 다 바꿔치기를 함, 그래서 Transaction commit을 할 때 반영이 되는 것임
- 즉 JPA가 위에서 작성한 코드를 merge 한 줄로 해결하는 것

```java
// 상품 저장
    public void save(Item item) {
        // Id가 null이면 아이템 저장(처음에 새로 생성한 객체는 id가 없으므로)
        if(item.getId() == null) {
            em.persist(item);
        } else {
            // 만약 Id가 있다면 merge를 함(업데이트와 비슷, 이미 DB 등록된 것을 어디서 가져온 것이므로)
            em.merge(item);
        }
    }
```

- 코드 동작방식은 마치 아래와 같음, findItem을 반환해준다는 것

```java
@Transactional // 변경 감지를 해서 업데이트 하기 위한 로직(준영속 컨텍스트에 대해)
    public Item updateItem(Long itemId, Book param) {
        // 먼저 아이템을 찾음, Id기반으로 실제 영속상태 엔티티를 찾아옴
        Item findItem = itemRepository.findOne(itemId);
        // 그 다음 넘겨받음 Book param에서 값을 가져와 findItem에 set을 해주면 됨, 이런식으로 수정할 것 다 반영해줌
        findItem.setPrice(param.getPrice());
        findItem.setName(param.getName());
        findItem.setStockQuantity(param.getStockQuantity());
        return findItem;
    }
```

- 근데 중요한 것은 위의 merge 부분의 item은 영속성 컨텍스트로 바뀌지 않음(파라미터로 넘어온 item)

![one](/img/Spring/WebLayer/eight.png)
![one](/img/Spring/WebLayer/nine.png)

- 그런데 여기서 병합은 조심할 부분이 있음, 위의 주의라고 쓴 대로 변경 감지는 원하는 속성만 선택해서 변경할 수 있지만, 병합은 모든 속성이 변경됨
- 이것이 왜 위험하냐면 병합시 값이 없으면 모두 null로 업데이트를 해버릴 수 있기 때문임
- 아래와 같이 만약 가격은 고정을 시킨다고 가정했을 때 price는 null이 되버림 수정을 안 건드리니깐
- 이렇게 되면 DB에 null로 업데이트가 되버림, null조차도 갈아끼워버리는 것임, 그래서 null로 업데이트 되버리는 것임, 바꿔서 처리는 할 수 있는데 그렇게 되버리면 점점 더 복잡해지는 것임

```java
// 수정하도록 맵핑함
    @PostMapping("items/{itemId}/edit")
    public String updateItem(@ModelAttribute("form") BookForm form) {

        Book book = new Book();
        book.setId(form.getId());
        book.setName(form.getName());
//        book.setPrice(form.getPrice());
                book.price = null;
        book.setStockQuantity(form.getStockQuantity());
        book.setAuthor(form.getAuthor());
        book.setIsbn(form.getIsbn());

        itemService.saveItem(book);
        return "redirect:/items";
    }
```

- 그런 경우를 방지하기 위해서는 불가피하게 merge가 아닌 변경감지를 써야함, 직접 조회를 해서 업데이트 할 필드를 가져와서 set을 해야함, 위에서 작성한대로, merge를 최대한 쓰지 않으려고 해야함, 한땀한땀 쓰려고 해야함
- 그리고 보통 업데이트는 단발성으로 하면 안됨, 의미있는 메소드를 만들어야지 위에처럼 set을 막 깔면 안됨, 메소드화 시켜줘야 변경지점이 다 엔티티로 가기 때문에, set을 써버리면 찾는데 한참 걸려버림, 메소드를 걸어두면 역추척하기 편하기 때문에

```java
@Transactional // 변경 감지를 해서 업데이트 하기 위한 로직(준영속 컨텍스트에 대해)
    public void updateItem(Long itemId, Book param) {
        // 먼저 아이템을 찾음, Id기반으로 실제 영속상태 엔티티를 찾아옴
        Item findItem = itemRepository.findOne(itemId);

                // 제대로 하기 위해서 메소드화 시키는게 좋음
                findItem.change(price, name, stockQuantity);

                // 단발성 지양해야하는 방식
        // 그 다음 넘겨받음 Book param에서 값을 가져와 findItem에 set을 해주면 됨, 이런식으로 수정할 것 다 반영해줌
        findItem.setPrice(param.getPrice());
        findItem.setName(param.getName());
        findItem.setStockQuantity(param.getStockQuantity());
        // 수정을 다 한 후 마지막에 별도로 리포지토리 불러서 save나 아무것도 안해도 됨
    }
```

![one](/img/Spring/WebLayer/ten.png)

- 그래서 위에서 설명한대로 하는 것이 가장 권장되는 방법임
- 컨트롤러에서 어설프게 만들지 말라는 것이 아래와 같이 Controller에서 Book 객체를 직접 만든 경우를 말함

```java
// 수정하도록 맵핑함
    @PostMapping("items/{itemId}/edit")
    public String updateItem(@ModelAttribute("form") BookForm form) {

        Book book = new Book();
        book.setId(form.getId());
        book.setName(form.getName());
        book.setPrice(form.getPrice());
        book.setStockQuantity(form.getStockQuantity());
        book.setAuthor(form.getAuthor());
        book.setIsbn(form.getIsbn());

        itemService.saveItem(book);
        return "redirect:/items";
    }
```

- 더 나은 설계는 아래와 같이해서 설계할 수 있음, itemService에 있는 updateItem을 활용하여서 매개변수로 받은 다음 갱신하는 것
- service 단위에서 아래와 같이 수정함

```java
@Transactional // 변경 감지를 해서 업데이트 하기 위한 로직(준영속 컨텍스트에 대해)
    public void updateItem(Long itemId, String name, int price, int stockQuantity) {
        // 먼저 아이템을 찾음, Id기반으로 실제 영속상태 엔티티를 찾아옴
        Item findItem = itemRepository.findOne(itemId);
        // 매개변수로 받아서 수정할 것 다 반영해줌
        findItem.setPrice(price);
        findItem.setName(name);
        findItem.setStockQuantity(stockQuantity);
        // 수정을 다 한 후 마지막에 별도로 리포지토리 불러서 save나 아무것도 안해도 됨
    }
```

- 그 다음 Controller에서 그 메소드를 그대로 쓰면 됨

```java
// 수정하도록 맵핑함
    @PostMapping("items/{itemId}/edit")
    public String updateItem(@PathVariable Long itemId, @ModelAttribute("form") BookForm form) {

        itemService.updateItem(itemId, form.getName(), form.getPrice(),form.getStockQuantity());
        return "redirect:/items";
    }
```

- 이런식으로 하면 훨씬 깔끔함, 어설프게 엔티티를 파라미터로 안 쓰고 필요한 데이터만 받은 것
- 업데이트 할 게 많다면 service 계층에 DTO를 하나 만들면 됨, 별도의 클래스로 뽑아서 즉, DTO에 getter, setter 선언을 해서 DTO를 참고해서 해당 값을 위처럼 받아서 넘겨주면 됨, 매개변수로 하는게 아니라 get, set Controller에서 쓰듯이