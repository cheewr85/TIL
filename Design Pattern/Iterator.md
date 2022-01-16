## Iterator
- 순서대로 지정해서 처리하기
```java
for(int i = 0; i < arr.length; i++) {
		System.out.println(arr[i]);
}
```

- 여기에서 사용되고 있는 변수 i의 기능을 추상화해서 일반화한 것을 디자인 패턴에서는 Iterator 패턴이라고 함
- Iterator 패턴이란 무엇인가 많이 모여있는 것들을 순서대로 지정하면서 전체를 검색하는 처리를 실행하기 위한 것임(반복자라고도 함)

### 예제
![one](/img/DesignPattern/Iterator/one.png)

- Aggregate 인터페이스는 요소들이 나열되어 있는 집합체를 나타냄
- Aggregate : 집합체를 나타내는 인터페이스
- Iterator : 하나씩 나열하면서 검색을 실행하는 인터페이스
    - Aggregate가 Iterator를 생성함
- Book : 책을 나타내는 클래스
- BookShelf : 서가를 나타내는 클래스
- BookShelfIterator : 서가를 검색하는 클래스
    - BookShelf가 books 필드로 Book을 가지고 있음 그리고 Aggregate 인터페이스를 구현함
    - BookShelfIterator가 bookShelf 필드로 BookShelf를 가지고 있음 그리고 Iterator 인터페이스를 구현함
    - 위와 같은 집약 관계에 있음

```java
public interface Aggregate {
		public abstract Iterator iterator();
}
```
```java
public interface Iterator {
		public abstract boolean hasNext();
		public abstract Object next();
}
```
- Aggregate 인터페이스에서 iterator 메소드 하나만 선언됨, 이는 집합체에 대응하는 Iterator를 1개 작성하기 위한 것
- 집합체를 하나씩 나열하고, 검색하고, 조사하고 싶을 때에는 iterator 메소드를 사용해서 Iterator 인터페이스를 구현한 클래스의 인스턴스를 1개 만듬
- Iterator 인터페이스는 요소를 하나씩 나열하면서 루프 변수와 같은 역할을 수행함
- 다음 요소가 존재하는지를 조사하기 위한 hasNext 메소드와 다음 요소를 얻기 위한 next 메소드 존재함, hasNext 메소드를 루프의 종료 조건으로 사용함
- next 메소드는 집합체의 요소를 1개 반환해줌, 해당 메소드 호출 시 정확히 다음 요소를 반환하도록 내부 상태를 다음으로 진행시켜 두는 역할이 숨어있음

```java
public class Book {
		private String name;
		public Book(String name) {
				this.name = name;
		}
		public String getName() {
				return name;
		}
}
```
```java
public class BookShelf implements Aggregate {
		private Book[] books;
		private int last = 0;
		public BookShelf(int maxsize) {
				this.books = new Book[maxsize];
		}
		public Book getBookAt(int index) {
				return books[index];
		}
		public void appendBook(Book book) {
				this.books[last] = book;
				last++;
		}
		public int getLength() {
				return last;
		}
		public Iterator iterator() {
				return new BookShelfIterator(this);
		}
}
```
```java
public class BookShelfIterator implements Iterator {
		private BookShelf bookShelf;
		private int index;
		public BookShelfIterator(BookShelf bookShelf) {
				this.bookShelf = bookShelf;
				this.index = 0;
		}
		public boolean hasNext() {
				if(index < bookShelf.getLength()) {
						return true;
				} else {
						return false;
				}
		}
		public Object next() {
				Book book = bookShelf.getBookAt(index);
				index++;
				return book;
		}
}
```
- Book 클래스는 책 이름만을 얻을 수 있음, 생성자에서 인스턴스를 초기화할 때 인수로 지정함
- BookShelf 클래스는 집합체로 다루기 위해서 Aggregate 인터페이스를 구현함, Aggregate 인터페이스에 선언되어 있던 iterator 메소드가 기술되어 있음
- books 필드는 Book의 배열임, 배열의 크기는 BookShelf의 인스턴스를 만들 때 지정함
- iterator 메소드는 BookShelfIterator라는 클래스의 인스턴스를 생성해서 그것을 반환함, 이 BookShelf의 Book을 하나씩 나열하고 싶을 때 iterator 메소드를 호출함
- BookShelfIterator를 Iterator 인터페이스를 구현함
- bookShelf 필드는 BookShelfIterator에서 검색할 BookShelf이고 index 필드는 현재 주목하고 있는 책을 가르키는 첨자임
- 생성자를 통해서 전달된 BookShelf 인스턴스를 bookShelf 필드에 저장하고 index를 0으로 초기화함
- hasNext 메소드를 구현함, 다음 책 있는지 조사하고 있으면 true, 없으면 false를 반환함, 이는 index가 bookShelf.getLength의 값보다 작은지 큰지로 판명함
- next 메소드는 현재 처리하고 있는 Book의 인스턴스를 반환하고 다음으로 진행시킴
- 반환값을 book이라는 변수에 저장해두고 index를 다음으로 진행시킴
- 이 index를 다음으로 진행시키는 것이 for 문의 i++에 해당함, 루프변수를 다음으로 진행시킨 것

```java
public class Main {
		public static void main(String[] args) {
				// BookShelf 인스턴스 생성과 함께 생성자에서 정의한대로 배열의 크기 4로 지정
				BookShelf bookShelf = new BookShelf(4);
				// appendBook 메소드 사용과 Book 인스턴스 생성 이름에 맞게 Book 생성해서 저장
				// BookShelf내에서 books필드에 맞게 인덱스와 배열에 들어가서 자동으로 반영
				bookShelf.appendBook(new Book("Around the World in 80 Days"));
				bookShelf.appendBook(new Book("Bible"));
				bookShelf.appendBook(new Book("Cinderella"));
				bookShelf.appendBook(new Book("Daddy-Long-Legs"));
				// 탐색을 위해서 Iterator 생성 및 bookShelf에 iterator 메소드 호출
				Iterator it = bookShelf.iterator();
				// BookShelf에 구현된 메소드 사용 hasNext를 통해서 배열 전부를 훑어볼 수 있음
				while (it.hasNext()) {
						// BookShelfIterator에 있는 next 사용 해당 인덱스의 Book을 return 해서 가져옴
						// while 문 안에 book에 저장
						Book book = (Book)it.next();
						// 받은 book에 대해서 출력을 함
						System.out.println(book.getName());
				}
		}
}
```

### 패턴의 등장인물
![one](/img/DesignPattern/Iterator/two.png)

- Iterator(반복자)의 역할
    - 요소를 순서대로 검색해가는 인터페이스(API)를 결정함
    - 예제에서 Iterator 인터페이스가 그 역할을 하고 다음 요소가 존재하는지를 얻기 위한 hasNext 메소드와 다음 요소를 얻기 위한 next 메소드를 결정함
- ConcreteIterator(구체적인 반복자)의 역할
    - Iterator가 결정한 인터페이스(API)를 실제로 구현함
    - 예제에서 BookShelfIterator가 그 역할을 함, 검색하기 위한 필요한 정보를 가지고 있어야함
    - BookShelf 클래스의 인스턴스는 bookShelf 필드에서 처리되고 있는 책은 index 필드에 기억되어 있음
- Aggregate(집합체)의 역할
    - Iterator 역할을 만들어내는 인터페이스(API)를 결정함
    - 내가 가지고 있는 요소를 순서대로 검색해 주는 사람을 만들어내는 메소드
    - 예제 프로그램에서 Aggregate 인터페이스가 이 역할을 담당하고 iterator 메소드를 결정함
- ConcreteAggregate(구체적인 집합체)의 역할
    - Aggregate 역할이 결정한 인터페이스(API)를 실제로 구현하는 일을 함
    - ConcreteIterator 역할의 인스턴스를 만들어냄
    - BookShelf 클래스가 이 역할을 담당하고 iterator 메소드를 구현함

## 사고력 키우기

### 구현에 상관없이 Iterator를 사용할 수 있음
- Iterator를 사용함으로써 구현과 분리해서 하나씩 셀 수 있음
- while 루프에서 BookShelf의 구현에는 의존하지 않음, 이 말은 BookShelf에서 Book이 아닌 Vector를 사용하더라도 BookShelf가 iterator 메소드를 가지고 있으므로 올바른 Iterator을 반환해 준다면 while 루프를 전혀 변경하지 않아도 동작을 함(it 을 활용한 로직을 그대로 사용 수정을 했어도)
- 이는 클래스의 재이용화를 촉진하고 그것은 클래스를 부품처럼 사용할 수 있게 하고, 하나의 부품을 수정해도 다른 부품에 큰 영향 없이 적은 수정만으로 끝낼 수 있다는 것을 의미함

### 추상 클래스나 인터페이스는 아무리 해도 서투른데
- 구체적인 클래스만 사용하면 클래스 간의 결합이 강해져서, 부품으로 재이용하는 일이 어려움
- 결합을 약하게 해서 부품으로 재이용하기 쉽도록 하기 위해 추상 클래스나 인터페이스를 도입함

### 복수의 Iterator
- 하나씩 나열하는 구조가 Aggregate 역할의 외부에 놓여있다는 것으로 하나의 ConcreteAggregate 역할에 대해서 복수의 ConcreteIterator 역할을 만들 수 있음

### Iterator의 다양한 종류
- 뒤에서 시작해서 역방향으로 진행, 정방향으로도, 역방향으로도 진행(next 메소드뿐만 아니라 previous 메소드도 가짐), 번호를 지정해서 그곳으로 점프함 등의 Iterator 클래스도 만들 수 있음

### deleteIterator는 필요없다
- Java에서는 사용되지 않는 인스턴스는 자동적으로 삭제됨(garbage collection), 따라서 iterator에 대응하는 deleteIterator 메소드는 필요없음

## 안드로이드에 응용
- 데이터 처리 등을 할 때 ArrayList를 사용하는 경우가 존재함, 이때 단순히 특정 요소 여러개를 삭제하기 위해서 반복문 루프 안에서 remove()를 하면 코드가 작동하지 않거나 에러가 나는 경우가 있음
- 장바구니 목록에서 체크한 상품들만 삭제한다고 할 때, 반복문 안에서 순서대로 ArrayList의 요소의 체크여부를 확인함, 요소가 체크되었을 때 삭제를 해야하는데 이렇게 지워버리면 다음 요소들의 순번이 하나씩 앞으로 오게됨, 그리고 또다시 삭제를 해야할 때 요소들의 순번이 바뀌어 있으므로 에러가 남, 이를 막기 위해서 Iterator를 사용함
```java
public interface Iterator {
    boolean hasNext(); 
    Object next();
    void remove();
}
/*
hasNext() : 읽어올 요소가 남아있는지 확인하는 메소드. 요소가 있으면 true, 없으면 false를 반환.
next() : 다음 요소를 반환.
remove() : next()로 읽어온 요소를 현재 컬렉션에서 제거. 
메소드 호출 순서 : hasNext() → next() → remove()
*/
```
```java
//방법1.

ArrayList<Integer> list = new ArrayList<Integer>();
for( Iterator<Integer> itr = list.iterator(); itr.hasNext(); )
{
  list.get( itr.next() );
}

//방법2.

ArrayList<Integer> list = new ArrayList<Integer>();
Iterator<Integer> itr = list.iterator();
while( itr.hasNext() )
{
  list.get( itr.next() );
}
```