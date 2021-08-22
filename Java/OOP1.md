### 1.객체지향언어

- 실제 세계는 사물(객체)로 이루어져 있으며, 발생하는 모든 사건들은 사물간의 상호작용
- 실제 사물의 속성과 기능을 분석하고 데이터(변수)와 함수로 정의하여서 활용하여 사용함
- 규칙들을 이용해서 코드 간에 서로 관계를 맺어 줌으로써 보다 유기적으로 프로그램을 구성하는것
- 코드의 재사용이 높음 → 새로운 코드를 작성할 때 기존의 코드를 이용하여 쉽게 작성할 수 있음
- 코드의 관리가 용이함 → 코드간의 관계를 이용해서 적은 노력으로 쉽게 코드를 변경할 수 있음
- 신뢰성이 높은 프로그래밍을 가능하게 함 → 제어자와 메서드를 이용해서 데이터를 보호하고 올바른 값을 유지하도록 하며, 코드의 중복을 제거하여 코드의 불일치로 인한 오작동을 방지할 수 있음
- 객체지향개념을 학습할 때 재사용성과 유지보수 그리고 중복된 코드의 제거의 관점으로 보면 됨
- 일단 프로그램을 기능적으로 완성한 다음 어떻게 하면 보다 객체지향적으로 코드를 개선할 수 있을지 고민하여 점차 개선해 나가는 것이 좋음

### 2.클래스와 객체

- 클래스
    - 클래스는 객체를 정의해놓은 것 또는 객체의 설계도 또는 틀이라고 정의할 수 있음
    - 객체를 생성하는데 사용되며, 객체는 클래스에 정의된 대로 생성됨
- 객체지향이론에서는 사물과 같은 유형적인 것뿐만 아니라, 개념이나 논리와 같은 무형적인 것들도 객체로 간주함
- 즉 프로그래밍에서는 클래스에 정의된 내용대로 메모리에 생성된 것을 뜻함
- 예를 들면 TV 설계도(클래스)는 TV라는 제품(객체)을 정의한 것이며 TV(객체)를 만드는데 사용됨
- 즉 클래스는 단지 객체를 생성하는데 사용될 뿐 객체 그 자체는 아님
- 이를 잘 생각해보면 제품을 만들 때마다 고민할 필요 없이 설계도대로만 만들면 되는 것임
- 그냥 클래스로부터 객체를 생성해서 사용하기만 하면 됨
- 인스턴스화
    - 클래스로부터 객체를 만드는 과정
- 인스턴스
    - 어떤 클래스로부터 만들어진 객체
- 객체는 모든 인스턴스를 대표하는 포괄적인 의미를 갖고 있고 인스턴스는 어떤 클래스로부터 만들어진 것인지를 강조하는 보다 구체적인 의미를 가지고 있음
- 클래스 → 인스턴스화 → 인스턴스(객체)
- 객체의 구성요소
    - 속성과 기능, 일반적으로 객체는 다수의 속성과 다수의 기능을 가짐
    - 객체는 속성과 기능의 집합이라고 할 수 있음
    - 객체가 가지고 있는 속성과 기능을 그 객체의 멤버라고 함
- 클래스에는 객체의 모든 속성과 기능이 정의되어있음, 클래스로부터 객체를 생성하면 클래스에 정의된 속성과 기능을 가진 객체가 만들어짐
- 속성은 주로 멤버변수로 기능은 주로 메서드로 사용함
- 속성(Property) → 멤버변수(member variable), 특성(attribute), 필드(field), 상태(state)
- 기능(function) → 메서드(method), 함수(function), 행위(behavior)
- 예시 - Tv 클래스

```java
Class Tv {
		// 속성 -> 변수
		String color; // 색깔
		boolean power; // 전원상태
		int channel; // 채널
	
		// 기능 -> 메서드
		void power() {power = !power; }
		void channelUp() { channel++; }
		void channelDown() { channel--; }
}
```

- 프로그래밍에 필요한 속성과 기능만을 선택하여 클래스를 작성하면 됨
- 각 변수의 자료형은 속성의 값에 알맞은 것을 선택해야함
- 인스턴스의 생성과 사용
- 위의 예시를 사용하면 Tv클래스 선언은 Tv 설계도를 작성한 것에 불과하므로 Tv인스턴스를 생성해야 제품(Tv)을 사용할 수 있음
- 일반적으로 아래와 같이 함

```java
// 클래스명 변수명; -> 클래스의 객체를 참조하기 위한 참조변수를 선언
// 변수명 = new 클래스명(); -> 클래스의 객체를 생성 후, 객체의 주소를 참조변수에 저장

Tv t; // Tv클래스 타입의 참조변수 t를 선언
t = new Tv(); // Tv인스턴스를 생성한 후, 생성된 Tv인스턴스의 주소를 t에 저장
```

- 예시 - Tv클래스 활용
- 아래와 같이 인스턴스를 생성하고 인스턴스 속성(channel)과 메서드(channelDown())을 사용함

```java
Class Tv {
		// 속성 -> 변수
		String color; // 색깔
		boolean power; // 전원상태(on/off)
		int channel; // 채널
	
		// 기능 -> 메서드
		void power() {power = !power; } // TV를 켜거나 끄는 기능을 하는 메서드
		void channelUp() { channel++; } // TV의 채널을 높이는 기능을 하는 메서드
		void channelDown() { channel--; } // TV의 채널을 낮추는 기능을 하는 메서드
}

class TvTest {
			public static void main(String args[]) {
						Tv t;  // Tv인스턴스를 참조하기 위한 변수 t를 선언
						t = new Tv();  // Tv인스턴스를 생성함
						t.channel = 7;  // Tv인스턴스의 멤버변수 channel의 값을 7로 함
						t.channelDown();  // Tv인스턴스의 메서드 ChannelDown()을 호출함
						System.out.println("현재 채널은 " + t.channel + " 입니다.");
			}
}
```

- 인스턴스는 오직 참조변수를 통해서만 다룰 수 있음, 위처럼 Tv인스턴스를 사용하려면, Tv클래스 타입의 참조변수가 필요한 것임
- 인스턴스는 참조변수를 통해서만 다룰 수 있으며, 참조변수의 타입은 인스턴스의 타입과 일치해야함
- 같은 클래스로부터 생성되었을지라도 각 인스턴스의 속성(멤버변수)은 서로 다른 값을 유지할 수 있으며, 메서드의 내용은 모든 인스턴스에 대해 동일함
- 즉 참조변수에는 하나의 값(주소)만이 저장될 수 있으므로 둘 이상의 참조변수가 하나의 인스턴스를 가리키는(참조하는)것은 가능하지만 하나의 참조변수로 여러 개의 인스턴스를 가리키는 것은 가능하지 않음
- 객체 배열
    - 객체 역시 배열로 다루는 것이 가능함, 객체 배열 안에 객체의 주소가 저장됨
    - 객체 배열은 참조변수들을 하나로 묶은 참조 변수 배열인 것
- 그저 객체를 다루기 위한 참조 변수들이 만들어진 것일 뿐, 객체는 저장되지 않음
- 객체를 생성해서 객체 배열의 각 요소에 저장하는 것을 잊으면 안됨
- 객체 배열도 같은 타입의 객체만 저장할 수 있음
- 예시

```java
class TvTest4 {
	public static void main(String args[]) {
		Tv[] tvArr = new Tv[3]; // 길이가 3인 Tv객체 배열
		
		// Tv객체를 생성해서 Tv객체 배열의 각 요소에 저장
		for(int i=0; i < tvArr.length; i++) {
				tvArr[i] = new Tv();
				tvArr[i].channel = i+10; // tvArr[i]의 channel에 i+10 저장
		}

		for(int i=0; i < tvArr.length; i++) {
				tvArr[i].channelUp(); // tvArr[i]의 메서드를 호출. 채널이 1증가
				System.out.printf("tvArr[%d].channel=%d%n",i, tvArr[i].channel);
		}

	}
}

class Tv {
			String color; // 색상
			boolean power; // 전원상태(on/off)
			int channel; // 채널
		
			void power() { power = !power; }
			void channelUp() { ++channel; }
			void channelDown() { --channel; }
}
```

- 클래스 - 데이터와 함수의 결합
    - 변수 - 하나의 데이터를 저장할 수 있는 공간
    - 배열 - 같은 종류의 여러 데이터를 하나의 집합으로 저장할 수 있는 공간
    - 구조체 - 서로 관련된 여러 데이터를 종류에 관계없이 하나의 집합으로 저장할 수 있는 공간
    - 클래스 - 데이터와 함수의 결합(구조체 + 함수)
- 데이터와 함수는 서로 관계가 깊다, 이를 클래스에 정의해서 함꼐 다루는 것임
- 클래스 - 사용자정의 타입
    - 프로그래머가 서로 관련된 변수들을 묶어서 하나의 타입으로 새로 추가하는 것을 사용자정의 타입이라고 함
    - 예를 들어 시간을 표현하기 위해서 Time 클래스를 정의해서 시,분,초를 처리할 수 있다
    - 이를 단순히 데이터만 구분하는 것에 그치지 않고 제어자와 메소드를 사용해서 클래스를 활용할 수 있다

    ```java
    public class Time {
    			private int hour;
    			private int minute;
    			private float second;
    		
    			public int getHour() { return hour; }
    			public int getMinute() { return minute; }
    			public float getSecond() { return second; }

    			public void setHour(int h) {
    						if (h < 0 || h > 23) return;
    						hour = h;
    			}
    			
    			public void setMinute(int m) {
    						if (m < 0 || m > 59) return;
    						minute = m;
    			}
    		
    			public void setSecond(float s) {
    						if (s < 0.0f || s > 59.99f) return;
    						second = s;
    			}
    }
    ```

- 제어자를 이용해서 변수의 값을 직접 변경하지 못하도록 하고 대신 메소드를 통해서 값을 변경하도록 함

### 3.변수와 메서드

- 멤버변수를 제외한 나머지 변수들은 모두 지역변수이며, 멤버변수 중 static이 붙은 것은 클래스변수, 붙지 않은 것은 인스턴스 변수임

```java
class Variables
{   /* 클래스 영역 */
		int iv; // 인스턴스 변수
		static int cv;  // 클래스 변수(static 변수, 공유변수)

		void method()
		{ /* 메서드 영역*/
			int lv = 0; // 지역변수
		}
}
```

- 클래스 변수
    - 선언위치 : 클래스 영역
    - 생성시기 : 클래스가 메모리에 올라갈 때
    - 인스턴스변수 앞에 static을 붙이기만 하면 됨
    - 모든 인스턴스가 공통된 저장공간(변수)을 공유하게 됨
    - 한 클래스의 모든 인스턴스들이 공통적인 값을 유지해야하는 속성일 경우 클래스 변수를 선언함
    - 인스턴스를 생성하지 않고도 바로 사용할 수 있음
    - 클래스이름.클래스변수(Variables.cv)
    - 클래스가 메모리에 로딩될 때 생성되어 프로그램이 종료될 때까지 유지되며 어디서나 접근할 수 있는 전역변수의 성격을 가짐
- 인스턴스 변수
    - 선언위치 : 클래스 영역
    - 생성시기 : 인스턴스가 생성되었을 때
    - 인스턴스 변수의 값을 읽어 오거나 저장하기 위해서는 인스턴스를 생성해야함
    - 인스턴스는 독립적인 저장공간을 가지므로 서로 다른 값을 가질 수 있음
    - 인스턴스마다 고유한 상태를 유지해야하는 속성의 경우, 인스턴스 변수로 선언함
- 지역 변수
    - 메서드 내에 선언되어 메서드 내에서만 사용가능함, 메서드 종료시 소멸되어 사용할 수 없음
    - for문, while문의 블럭 내에 선언된 지역변수는 선언된 블럭 내에서만 사용 가능함, 블럭을 벗어나면 소멸되어 사용할 수 없게 됨
- 예를 들어 카드 클래스를 작성하기 위해서 카드의 무늬, 숫자, 폭, 높이를 생각할 때, 무늬와 숫자는 가변적이므로 인스턴스 변수로 선언하여서 유동적으로 쓸 수 있지만 높이와 폭은 고정값이므로 이를 클래스 변수로 정하여 공통적으로 같은 값을 유지해야한다

```java
class CardTest {
	public static void main(String args[]) {
			System.out.println("Card.width = " + Card.width);
			System.out.println("Card.height = " + Card.height);

			Card c1 = new Card();
			c1.kind = "Heart";
			c1.number = 7;

			Card c2 = new Card();
			c2.kind = "Spade";
			c2.number = 4;
			
			System.out.println("c1의 width와 height를 각각 50, 80으로 변경합니다.");
			c1.width = 50;
			c1.height = 80;
	}
}

class Card {
		String kind;
		int number;
		static int width = 100;
		static int height = 250;
}
```

- 인스턴스변수는 인스턴스가 생성될 때 마다 생성되므로 인스턴스마다 각기 다른 값을 유지할 수 있지만, 클래스 변수는 모든 인스턴스가 하나의 저장공간을 공유하므로, 항상 공통된 값을 갖는다
- 메서드
    - 특정 작업을 수행하는 일련의 문장들을 하나로 묶은 것
    - 작업을 수행하는데 필요한 값만 넣고 원하는 결과를 얻는 것, 넣을 값(입력)과 반환하는 결과(출력)만 알면 됨
    - 메서드를 내부가 보이지 않는 블랙박스라고도 함
- 메서드를 사용하는 이유
- 높은 재사용성
    - 한 번 만들어 놓은 메서드는 몇 번이고 호출할 수 있으며, 다른 프로그램에서도 사용이 가능함
- 중복된 코드의 제거
    - 반복되는 문장들을 묶어서 하나의 메서드로 작성해 놓으면, 반복되는 문장들 대신 메서드를 호출하는 한 문장으로 대체할 수 있음
- 프로그램의 구조화
    - 큰 규모의 프로그램에서는 문장들을 작업단위로 나눠서 여러 개의 메서드에 담아 프로그램의 구조를 단순화 시키는 것이 필수적임
- 메서드의 선언과 구현
- 선언부와 구현부로 이루어져 있음
- 선언부
    - 메서드의 이름과 매개변수 선언, 그리고 반환타입으로 구성되어 있음
    - 메서드가 작업을 수행하기 위해 어떤 값들을 필요로 하고 작업의 결과로 어떤 타입의 값을 반환하는지에 대한 정보를 제공함
    - 매개변수 선언 → 메서드가 작업을 수행하는데 필요한 값들(입력)을 제공받기 위한 것, 필요한 갯수만큼 쉼표로 구분함, 변수타입이 같아도 생략이 불가능함
    - 메서드의 이름 → 변수의 명명규칙대로 작성하면 됨, 메서드의 기능을 쉽게 알 수 있도록 함축적이면서도 의미있는 이름을 짓도록 해야함
    - 반환타입 → 작업수행 결과(출력)인 반환값의 타입을 적음, 반환값이 없는 경우 void를 적어야함
- 구현부
    - 메서드를 호출했을 때 수행될 문장들을 넣음
    - return문 → void가 아닌 경우 return 반환값;이 반드시 포함되야함, 이 값의 타입은 반환타입과 일치하거나 적어도 자동 형변환이 가능한 것이어야 함, 단 하나의 값만 반환할 수 있음
    - 지역변수 → 서로 다른 메서드라면 같은 이름의 변수를 선언해도 됨, 메서드 내에 선언된 변수를 지역변수라고 함
- 메서드의 호출
- 메서드를 호출해야 구현부 문장들이 수행됨
- 메서드 호출 시 괄호()안에 지정해준 값들을 인자 또는 인수라고 하는데, 인자의 개수와 순서는 호출된 메서드에 선언된 매개변수와 일치해야함
- 선언된 매개변수보다 많은 값을 괄호에 넣거나 타입이 다른 값을 넣으면 컴파일러 에러가 생김
- 메서드 실행흐름

```java
Mymath mm = new Mymath(); // 먼저 인스턴스를 생성

long value = mm.add(1L, 2L); // 메서드를 호출함

long add(long a, long b) {
				long result = a + b;
				return result;
}
```

- 위처럼 메서드를 호출하면 호출시 지정한 1L, 2L이 메서드 add의 매개변수 a,b에 각각 복사(대입)됨 → 메서드 add의 괄호{}안에 있는 문장들이 순서대로 수행됨 → 메서드 add의 모든 문장이 실행되거나 return문을 만나면, 호출한 메서드(main 메서드)로 되돌아와서 이후의 문장들을 실행함
- 메서드가 호출되면 지금까지 실행 중이던 메서드는 실행을 잠시 멈추고 호출된 메서드의 문장들이 실행됨, 호출된 메서드의 작업이 모두 끝나면, 다시 호출한 메서드로 돌아와 이후의 문장들을 실행함
- 위의 long value 역시 mm.add(1L,2L) 실행후 결과값인 3L이 반환되어 해당 값을 long value에 저장되는 것임
- 메서드는 호출시 넘겨받은 값으로 연산을 수행하고 그 결과를 반환하면서 종료됨

```java
double result4 = mm.divide(5L, 3L);

double divide(double a, double b) {
			return a / b;
}
```

- 위처럼 굳이 형이 일치하지 않아도 long형이 double형 변수에 저장되는 것과 같아서 자동으로 형변환이 일어난다
- return문
- 현재 실행중인 메서드를 종료하고 호출한 메서드로 돌아감
- 원래는 반환값의 유무에 관계없이 모든 메서드에는 적어도 하나의 return문이 있어야함, void의 경우에도 컴파일러가 알아서 메서드의 마지막에 return;을 자동적으로 추가함
- 반환값이 있는 타입에서는 반드시 반환값이 있어야 함
- 반환값으로 항상 변수를 쓰는 것은 아니다 수식을 쓴다면 여기서 이 수식을 계산한 결과를 반환함
- 매개변수의 유효성 검사
- 매개변수가 유효하지 않을떄 메서드를 종료하기 위해서 return 0;를 쓴다, 작업을 중단하고 호출한 메서드로 되돌아가야 함
- JVM의 메모리 구조
    - 메서드 영역 : 프로그램 실행 중 어떤 클래스가 사용되면, JVM은 해당 클래스의 클래스파일을 읽어서 분석하여 클래스에 대한 정보(클래스 데이터)를 이곳에 저장함, 이 때 그 클래스의 클래스변수도 이 영역에 함께 생성됨
    - 힙 : 인스턴스가 생성되는 공간, 프로그램 실행 중 생성되는 인스턴스는 모두 이곳에 생성됨, 인스턴스변수들이 생성되는 공간임
    - 호출스택 : 메서드의 작업에 필요한 메모리 공간을 제공함, 메서드가 호출되면, 호출스택에 호출된 메서드를 위한 메모리가 할당되며, 이 메모리는 메서드가 작업을 수행하는 동안 지역변수들과 연산의 중간결과 등을 저장하는데 사용됨, 메서드가 작업을 마치면 할당되었던 메모리공간은 반환되어 비워짐
- 메서드가 호출되면 수행에 필요한 만큼의 메모리를 스택에 할당받음
- 메서드가 수행을 마치고 나면 사용했던 메모리를 반환하고 스택에서 제거됨
- 호출스택의 제일 위에 있는 메서드가 현재 실행중인 메서드임
- 아래에 있는 메서드가 바로 위의 메서드를 호출한 메서드임
- 기본형 매개변수와 참조형 매개변수
- 기본형 매개변수 → 변수의 값을 읽기만 할 수 있다(read only)
- 참조형 매개변수 → 변수의 값을 읽고 변경할 수 있다(read & write)

```java
class Data { int x; }

class PrimitiveParamEx {
	public static void main(String[] args) {
			Data d = new Data();
			d.x = 10;
			System.out.println("main() : x = " + d.x);
	
			change(d.x);
			System.out.println("After change(d.x)");
			System.out.println("main() : x = " + d.x);
	}

	static void change(int x) {
			x = 1000;
			System.out.println("change() : x = " + x);
	}
} 
```

- 위의 경우에는 d.x의 값이 변경된 것이 아니라 매개변수 x의 값이 변경된 것임

```java
class Data { int x; }

class PrimitiveParamEx {
	public static void main(String[] args) {
			Data d = new Data();
			d.x = 10;
			System.out.println("main() : x = " + d.x);
	
			change(d);
			System.out.println("After change(d.x)");
			System.out.println("main() : x = " + d.x);
	}

	static void change(Data d) {
			d.x = 1000;
			System.out.println("change() : x = " + d.x);
	}
} 
```

- 위의 경우에는 매개변수가 참조형이라서 값이 저장된 주소를 넘겨주었기 때문에 값을 변경이 가능한 것임
- 배열 역시도 이와 같이 참조형으로 넘겨주는 것임, 간단한 처리할 때는 클래스보다 배열이 나을 수도 있음
- 참조형 반환타입
- 매개변수뿐만 아니라 반환타입도 참조형이 될 수 있음, 모든 참조형 타입의 값은 객체의 주소임

```java
class Data { int x; }

class PrimitiveParamEx {
	public static void main(String[] args) {
			Data d = new Data();
			d.x = 10;
	
			Data d2 = copy(d); // 반환타입이 Data이므로 호출결과 저장하는 변수 역시 Data 타입
			System.out.println("d.x = " + d.x);
			System.out.println("d2.x = " + d2.x);
	}

	static Data copy(Data d) {
			Data tmp = new Data(); // 새로운 객체 tmp를 생성함
			tmp.x = d.x; // d.x의 값을 tmp.x에 복사함

			return tmp; // 복사한 객체의 주소를 반환함
	}
} 
```

- 위처럼 copy메서드는 새로운 객체를 생성한 다음에, 매개변수로 넘겨받은 객체에 저장된 값을 복사해서 반환했다, 반환하는 값이 Data 객체의 주소이므로 반환타입이 Data인 것임
- 반환타입이 참조형이라는 것은 메서드가 객체의 주소를 반환한다는 것을 의미함
- 재귀호출
- 메서드가 자신을 다시 호출하는 것을 재귀호출이라고 함
- 클래스 메서드(static 메서드)와 인스턴스 메서드
- 인스턴스 메서드는 인스턴스 변수와 관련된 작업을 하는, 즉 메서드의 작업을 수행하는데 인스턴스 변수를 필요로 하는 메서드임
- 인스턴스와 관계없는(인스턴스 변수나 인스턴스 메서드를 사용하지 않는) 메서드를 클래스 메서드(static메서드)로 정의함
- 클래스를 설계할 때, 멤버변수 중 모든 인스턴스에 공통으로 사용하는 것에 static을 붙임
    - 생성된 각 인스턴스는 서로 독립적이기 때문에 각 인스턴스 변수(iv)는 서로 다른 값을 유지함, 그러나 모든 인스턴스에서 같은 값이 유지되어야 하는 변수는 static을 붙여서 클래스 변수로 정의함
- 클래스 변수(static변수)는 인스턴스를 생성하지 않아도 사용할 수 있음
    - static이 붙은 변수(클래스변수)는 클래스가 메모리에 올라갈 때 이미 자동적으로 생성되기 때문임
- 클래스 메서드(static메서드)는 인스턴스 변수를 사용할 수 없다
    - 인스턴스변수는 인스턴스가 반드시 존재해야만 사용할 수 있는데 클래스메서드는 인스턴스 생성 없이 호출가능하므로 클래스 메서드가 호출되었을 때 인스턴스가 존재하지 않을 수도 있음, 그래서 클래스 메서드에서 인스턴스 변수 사용을 금지함
    - 반면에 인스턴스 변수나 인스턴스 메서드에서는 static이 붙은 멤버들을 사용하는 것이 언제나 가능함, 인스턴스 변수가 존재한다는 것은 static 변수가 이미 메모리에 존재한다는 것을 의미함
- 메서드 내에서 인스턴스 변수를 사용하지 않는다면, static을 붙이는 것을 고려함
    - 메서드 작업내용 중에서 인스턴스 변수를 필요로 하면 static을 붙일 수 없음, 반대의 경우에는 static을 붙임으로써 호출시간이 짧아져 성능이 향상됨
- 클래스의 멤버변수 중 모든 인스턴스에 공통된 값을 유지해야하는 것이 있는지 살펴보고 있으면, static을 붙여줌
- 작성한 메서드 중에서 인스턴스 변수나 인스턴스 메서드를 사용하지 않는 메서드에 static을 붙일 것을 고려함
- 클래스 멤버와 인스턴스 멤버간의 참조와 호출

### 4.오버로딩(Overloading)

- 자바에서는 한 클래스 내에 이미 사용하려는 이름과 같은 이름을 가진 메서드가 있더라도 매개변수의 개수 또는 타입이 다르면, 같은 이름을 사용해서 메서드를 정의할 수 있음
- 한 클래스 내에 같은 이름의 메서드를 여러 개 정의하는 것을 메서드 오버로딩 또는 간단히 오버로딩이라고 함
- 하나의 메서드 이름으로 여러 기능을 구현함
- 오버로딩의 조건
    - 메서드 이름이 같아야 함
    - 매개변수의 개수 또는 타입이 달라야 함
    - 매개변수에 의해서만 구별됨, 반환 타입은 오버로딩을 구현하는데 아무런 영향을 주지 못함
- 실제 println() 함수를 치면 자동완성으로 매우 많은 함수가 있음, 이것이 바로 오버로딩이 된 것임
- 같은 기능을 하는 메서드들에 대해서 이름을 줄이고 오류의 가능성을 줄인다
- 메서드의 이름을 절약할 수 있다
- 가변인자(varargs)와 오버로딩
- 매개변수 개수를 동적으로 지정해줄 수 있는데 이 기능을 가변인자라고 함
- 가변인자는 '타입...변수명'과 같은 형식으로 선언함, 가변인자는 매개변수 중에서 제일 마지막에 선언해야함

```java
public PrintStream printf(String format, Object... args) { ... }
```

- 만일 여러 문자열을 하나로 결합하여 반환하는 concatenate 메서드를 작성한다면, 매개변수의 개수를 다르게 해서 여러 개의 메서드를 작성할 필요없이 가변인자를 사용하면 메서드 하나로 간단히 대체할 수 있음

```java
String concatenate(String... str) { ... }
```

- 이렇게 하면 이 메서드를 호출할 때는 아래와 같이 인자의 개수를 가변적으로 할 수 있음

```java
System.out.println(concatenate());
System.out.println(concatenate("a"));
System.out.println(concatenate("a", "b"));
System.out.println(concatenate(new String[]{"A", "B"});
```

- 가변인자는 내부적으로 배열을 이용한다, 매개변수의 타입을 배열로 하는 경우는 반드시 인자를 지정해줘야하는 번거로움이 존재한다

### 5.생성자(Constructor)

- 생성자는 인스턴스가 생성될 때 호출되는 인스턴스 초기화 메서드임, 인스턴스 변수의 초기화 작업에 주로 사용됨, 인스턴스 생성 시 실행되어야 할 작업을 위해서도 사용됨
- 메서드처럼 클래스 내에 선언되며 리턴값이 없음, 아무것도 적지 않음
- 생성자의 이름은 클래스 이름과 같아야함, 생성자는 리턴 값이 없음
- 생성자는 인스턴스를 생성하는 것이 아님
- 인스턴스를 생성할 때는 반드시 클래스 내에 정의된 생성자 중의 하나를 선택하여 지정해주어야 함
- 모든 클래스는 반드시 하나 이상의 생성자가 정의되어 있어야 함
- 컴파일러가 기본 생성자를 제공하기 때문에 클래스에 생성자를 정의하지 않고도 인스턴스를 생성할 수 있었음
- 특별히 인스턴스 초기화 작업이 요구되어지지 않는다면 생성자를 정의하지 않고 컴파일러가 제공하는 기본 생성자를 사용하는 것도 좋음
- 기본 생성자가 컴파일러에 의해서 추가되는 경우는 클래스에 정의된 생성자가 하나도 없을 때 분이다
- 매개변수가 있는 생성자
- 생성자도 메서드처럼 매개변수를 선언하여 호출 시 값을 넘겨받아서 인스턴스의 초기화 작업에 사용할 수 있음
- 인스턴스마다 각기 다른 값으로 초기화되어야 하는 경우가 많기 때문에 매개변수를 사용한 초기화가 매우 유용함
- 아래의 예시처럼 따로 초기화해줄 필요 없이 매개변수가 있는 생성자를 사용하면 인스턴스를 생성하는 동시에 훨씬 더 편하게 초기화할 수 있다

```java
class Car {
		String color; // 색상
		String gearType; // 변속기 종류 - auto(자동), manual(수동)
		int door; // 문의 개수
		
		Car() {}
		Car(String c, String g, int d) {
				color = c;
				gearType = g;
				door = d;
		}
}

class CarTest {
		public static void main(String[] args) {
			Car c1 = new Car();
			c1.color = "white";
			c1.gearType = "auto";
			c1.door = 4;
		
			Car c2 = new Car("white", "auto", 4);
			
			System.out.println("c1의 color=" + c1.color + ", gearType=" + c1.gearType+ ", door="+c1.door);
			System.out.println("c2의 color=" + c2.color + ", gearType=" + c2.gearType+ ", door="+c2.door);
		}
}
```

- 생성자에서 다른 생성자 호출하기 - this(), this
- 생성자 간에도 서로 호출이 가능함, 단 생성자의 이름으로 클래스이름 대신 this를 사용함 + 한 생성자에서 다른 생성자를 호출할 때는 반드시 첫 줄에서만 호출이 가능함
- 생성자 내에서 다른 생성차 호출 시에는 클래스이름 대신 this를 사용해야함

```java
class Car {
	String color; // 색상
	String gearType; // 변속기 종류 - auto(자동), manual(수동)
	int door; // 문의 개수

	Car() {
			this("white", "auto", 4); // Car(String color, String gearType, int door)를 호출
	}

	Car(String color) {
			this(color, "auto", 4);
	}
	
	Car(String color, String gearType, int door) {
			this.color = color;
			this.gearType = gearType;
			this.door = door;
	}
}

class CarTest2 {
		public static void main(String[] args) {
				Car c1 = new Car();
				Car c2 = new Car("blue");

				System.out.println("c1의 color=" + c1.color + ", gearType=" + c1.gearType+ ", door="+c1.door);
				System.out.println("c2의 color=" + c2.color + ", gearType=" + c2.gearType+ ", door="+c2.door);
		}
}
```

- 여기서 this.color 부분은 인스턴스 변수이고 color는 생성자의 매개변수로 정의된 지역변수임
- 이렇게 구분함으로써 구분이 가능함
- 생성자의 매개변수로 인스턴스변수들의 초기값을 제공받는 경우가 많기 때문에 매개변수와 인스턴스변수의 이름이 일치하는 경우가 자주 있음, 이때 this를 사용해서 구별되도록 하는 것이 의미가 더 명확하고 이해하기 쉬움
- this → 인스턴스 자신을 가리키는 참조변수, 인스턴스의 주소가 저장되어 있음, 모든 인스턴스메서드에 지역변수로 숨겨진 채로 존재함
- this(), this(매개변수) → 생성자, 같은 클래스의 다른 생성자를 호출할 때 사용됨
- 생성자를 이용한 인스턴스의 복사
- 현재 사용하고 있는 인스턴스와 같은 상태를 갖는 인스턴스를 하나 더 만들고자 할 때 생성자를 이용할 수 있음, 두 인스턴스가 같은 상태를 갖는다는 것은 두 인스턴스의 모든 인스턴스 변수(상태)가 동일한 값을 갖고 있다는 것을 뜻함
- 어떤 인스턴스의 상태를 전혀 알지 못해도 똑같은 상태의 인스턴스를 추가로 생성할 수 있음

```java
class Car {
	String color; // 색상
	String gearType; // 변속기 종류 - auto(자동), manual(수동)
	int door; // 문의 개수

	Car() {
			this("white", "auto", 4); // Car(String color, String gearType, int door)를 호출
	}

	Car(Car c) { // 인스턴스의 복사를 위한 생성자
			color = c.color;
			gearType = c.gearType;
			door = c.door;
	}
	
	Car(String color, String gearType, int door) {
			this.color = color;
			this.gearType = gearType;
			this.door = door;
	}
}

class CarTest3 {
		public static void main(String[] args) {
				Car c1 = new Car();
				Car c2 = new Car(c1);

				System.out.println("c1의 color=" + c1.color + ", gearType=" + c1.gearType+ ", door="+c1.door);
				System.out.println("c2의 color=" + c2.color + ", gearType=" + c2.gearType+ ", door="+c2.door);

				c1.door = 100;
				System.out.println("c1.door=100; 수행 후");
				System.out.println("c1의 color=" + c1.color + ", gearType=" + c1.gearType+ ", door="+c1.door);
				System.out.println("c2의 color=" + c2.color + ", gearType=" + c2.gearType+ ", door="+c2.door);
		}
}
```

- 위처럼 인스턴스 c2는 c1을 복사하여 생성된 것이므로 서로 같은 상태를 갖지만, 서로 독립적으로 메모리공간에 존재하는 별도의 인스턴스이므로 c1의 값들이 변경되어도 c2는 영향을 받지 않음
- 인스턴스를 생성할 때는 다음의 2가지 사항을 결정해야함
    - 클래스 - 어떤 클래스의 인스턴스를 생성할 것인가?
    - 생성자 - 선택한 클래스의 어떤 생성자로 인스턴스를 생성할 것인가?

### 6.변수의 초기화

- 변수의 초기화
- 변수를 선언하고 처음으로 값을 저장하는 것을 변수의 초기화라고 함
- 가능하면 선언과 동시에 적절한 값으로 초기화 하는 것이 바람직함
- 지역변수는 사용하기 전에 반드시 초기화 해야함
- 멤버변수(클래스변수와 인스턴스변수)와 배열의 초기화는 선택적이지만, 지역변수의 초기화는 필수적임
- 멤버변수의 초기화 방법
- 명시적 초기화, 생성자, 초기화 블럭(인스턴스 초기화 블럭, 클래스 초기화 블럭)
- 명시적 초기화
- 변수를 선언과 동시에 초기화하는 것을 명시적 초기화라고 함, 가장 기본적이며서도 간단한 초기화 방법임
- 보다 복잡한 초기화 작업이 필요할 때는 초기화 블럭 또는 생성자를 사용해야함
- 초기화 블럭
- 클래스 초기화 블럭은 클래스변수의 초기화에 사용되고, 인스턴스 초기화 블럭은 인스턴스 변수의 초기화에 사용됨
- 블럭을 만들고 그 안에 코드를 작성하기만 하면 됨, 생성자보다 인스턴스 초기화 블럭이 먼저 수행됨

```java
class BlockTest {
	static {
			// 클래스 초기화 블럭
			System.out.println("static { }");
	}
	
	{
			// 인스턴스 초기화 블럭
			System.out.println("{ }");
	}
	
	public BlockTest() {
			System.out.println("생성자");
	}

	public static void main(String args[]) {
			System.out.println("BlockTest bt = new BlockTest(); ");
			BlockTest bt = new BlockTest();
		
			System.out.println("BlockTest bt2 = new BlockTest(); ");
			BlockTest bt2 = new BlockTest();
	}
}
```

```java
static { }
BlockTest bt = new BlockTest();
{ }
생성자
BlockTest bt2 = new BlockTest();
{ }
생성자
```

- 예제가 실행되면 위와 같이 BlockTest가 메모리에 로딩될 때, 클래스 초기화 블럭이 가장 먼저 수행되어 static { }이 화면에 출력되고 그 다음 main 메소드가 수행되어 BlockTest 인스턴스가 생성되며서 인스턴스 초기화 블럭이 먼저 수행되고, 끝으로 생성자가 수행됨
- 클래스 초기화 블럭은 처음 메모리에 로딩될 때 한 번만 수행되었지만, 인스턴스 초기화 블럭은 인스턴스가 생성될 때 마다 수행되었음
- 멤버변수의 초기화 시기와 순서
- 클래스변수의 초기화시점 : 클래스가 처음 로딩될 때 단 한 번 초기화 됨
- 인스턴스변수의 초기화시점 : 인스턴스가 생성될 때마다 각 인스턴스별로 초기화가 이루어짐
- 클래스변수의 초기화순서 : 기본값 → 명시적초기화 → 클래스 초기화 블럭
- 인스턴스변수의 초기화순서 : 기본값 → 명시적초기화 → 인스턴스 초기화 블럭 → 생성자