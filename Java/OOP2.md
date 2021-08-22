### 1.상속

- 기존의 클래스를 재사용하여 새로운 클래스를 작성하는 것
- 적은 양의 코드로 새로운 클래스를 만들고 코드를 공통적으로 관리할 수 있기 때문에 코드 추가 및 변경이 매우 용이함
- 사용법은 아래와 같음, extends 키워드와 함께 상속을 해 줌

```java
class Parent { }
class Child extends Parent { }
```

- 상속해주는 클래스를 조상 클래스(부모 클래스, 상위 클래스, 기반 클래스)라고 하고 상속 받는 클래스를 자손 클래스(자식 클래스, 하위 클래스, 파생된 클래스)라고 함
- 자손 클래스는 조상 클래스의 모든 멤버를 상속받기 때문에 Child 클래스는 Parent 클래스의 멤버들을 포함한다고 할 수 있음(확장성은 Child가 가지고 있음, 물론 Parent도 확장가능)

```java
class Parent {
		int age;
}

class Child extends Parent { 
		void play() {
				System.out.println("놀자~");
		}
}
```

- 위 같이 age라는 정수형 변수를 멤버 변수에 추가하면 자손 클래스 역시 자동적으로 age라는 멤버 변수가 추가됨
- 여기서 자손 클래스에 메소드를 추가하여도 이것은 조상 클래스에게는 영향을 주지는 못함
- 결과적으로 자손 클래스는 조상 클래스의 모든 멤버를 상속 받으므로 항상 조상 클래스보다 같거나 많은 멤버를 가짐, 상속을 거듭할수록 상속받는 클래스의 멤버 개수는 점점 늘어남
- 상속을 받는다는 것은 조상 클래스를 확장한다는 의미로 해석할 수 있음
- 생성자와 초기화 블럭은 상속되지 않음, 멤버만 상속됨, 자손 클래스의 멤버 개수는 조상 클래스보다 항상 같거나 많음
- 클래스 간의 관계에서 형제관계는 없음, 부모와 자식의 관계(상속관계)만이 존재함
- 만일 상속받은 자손 클래스들이 공통적으로 추가해야하는 것이 있다면 이 것을 조상 클래스에 추가하면 좋음
- 같은 내용의 코드를 하나 이상의 클래스에 중복적으로 추가해야하는 경우에는 상속관계를 이용해서 코드의 중복을 최소화할 수 있음
- 조상 클래스만 변경해도 모든 자손 클래스에, 자손의 자손 클래스에까지 영향을 미치므로 클래스간의 상속관계를 맺어 주면 자손 클래스들의 공통적인 부분은 조상 클래스에서 관리하고 자손 클래스는 자신에 정의된 멤버들만 관리하면 되므로 각 클래스의 코드가 적어져서 관리가 쉬워짐

```java
class Tv {
	boolean power; // 전원상태(on/off)
	int channel; // 채널

	void power() { power = !power; }
	void channelUp() { ++channel;  }
	void channelDown() { --channel; }
}

class CaptionTv extends Tv {
	boolean caption; // 캡션상태(on/off)
	void displayCaption(String text) {
		if (caption) { // 캡션 상태가 on(true)일때만 text를 보여줌
				System.out.println(text);
		}
	}
}

class CaptionTvTest {
	public static void main(String args[]) {
		CaptionTv ctv = new CaptionTv();
		ctv.channel = 10; // 조상 클래스로부터 상속받은 멤버
		ctv.channelUp(); // 조상 클래스로부터 상속받은 멤버
		System.out.println(ctv.channel);
		ctv.displayCaption("Hello, World");
		ctv.caption = true; // 캡션(자막)기능을 켠다
		ctv.displayCaption("Hello, World");
	}
}
```

- 자손 클래스의 인스턴스를 생성하면 조상 클래스의 멤버와 자손 클래스의 멤버가 합쳐진 하나의 인스턴스가 생성됨

### 포함관계

- 클래스간에 포함관계를 맺어주는 것, 한 클래스의 멤버변수로 다른 클래스 타입의 참조변수를 선언하는 것을 뜻함

```java
class Circle {
		int x; // 원점의 x좌표
		int y; // 원점의 y좌표
		int r; // 반지름(raidus)
}
```

```java
class Point {
		int x; // x좌표
		int y; // y좌표
}
```

- 여기서 Point 클래스를 재사용해서 Circle 클래스를 작성할 수 있음

```java
class Circle {
		Point c = new Point(); // 원점
		int r;
}
```

- 하나의 거대한 클래스를 작성하는 것보다 단위별로 여러 개의 클래스를 작성한 다음, 이 단위 클래스들을 포함관계로 재사용하면 보다 간결하고 손쉽게 클래스를 작성할 수 있음

### 클래스간의 관계 결정하기

- 위에 예시를 생각해서 클래스 간의 상속관계와 포함관계를 다시 한 번 생각해본다면
- 이 두 관계가 어떤 상태에 놓였는지에 따라서 포함관계를 둘 것인지 고려해야한다
- 예를 들어 SportsCar는 Car이다인 경우는 SportsCar 클래스가 Car 클래스를 상속하고 상속관계에 있다고 보는 것이 맞지만
- Deck은 Card를 가지고 있다라고 하면 Deck클래스에 Card 클래스를 포함시켜야 한다

```java
class DrawShape {
    public static void main(String[] args) {
        Point[] p = {   new Point(100, 100),
                        new Point(140, 50),
                        new Point(200,100)
        };
        
        Triangle t = new Triangle(p);
        Circle c = new Circle(new Point(150, 150), 50);
        
        t.draw(); // 삼각형을 그림
        c.draw(); // 원을 그림
    }
}

class Shape {
    String color = "black";
    void draw() {
        System.out.printf("[color=%s]%n", color);
    }
}

class Point {
    int x;
    int y;
    
    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
    Point() {
        this(0,0);
    }
    
    String getXY() {
        return "("+x+","+y+")"; // x와 y의 값을 문자열로 반환
    }
}

class Circle extends Shape {
    Point center; // 원의 원점좌표
    int r; // 반지름
    
    Circle() {
        this(new Point(0, 0), 100); // Circle(Point center, int r)를 호출
    }
    
    Circle(Point center, int r) {
        this.center = center;
        this.r = r;
    }
    
    void draw() {
        // 원을 그리는 대신에 원의 정보를 출력함
        System.out.printf("[center=(%d %d), r=%d, color=%s]%n", center.x, center.y, r, color);
    }
}

class Triangle extends Shape {
    Point[] p = new Point[3]; // 3개의 Point 인스턴스를 담을 배열을 생성함
    
    Triangle(Point[] p) {
        this.p = p;
    }
    
    void draw() {
        System.out.printf("[p1=%s, p2=%s, p3=%s, color=%s]%n",p[0].getXY(), p[1].getXY(), p[2].getXY(), color);
    }
}
```

- 위처럼 원은 도형이고 원은 점을 가지고 있다, 즉 클래스간의 관계를 맺는데 있어서 Circle과 Shape은 상속관계를 Point와는 포함관계로 정의를 할 수 있고, 이 관계에 따라서 포함관계를 잘 고려해야함

### 단일 상속

- 자바에서는 오직 단일 상속만을 허용함 즉, 둘 이상의 클래스로부터 상속받을 수 없음
- 이를 적용하기 위해서는 아래와 같이 할 수 있음

```java
class Tv {
	boolean power; // 전원상태(on/off)
	int channel; // 채널

	void power() { power = !power; }
	void channelUp() { ++channel;  }
	void channelDown() { -- channel; }
}

class VCR { 
	boolean power;
	int counter = 0;
	void power() { power = !power; }
	void play() { }
	void stop() { }
	void rew() { }
	void ff() { }
}

class TVCR extends Tv {
		VCR vcr = new VCR();
		
		void play() {
			vcr.play();
		}
		
		void stop() {
			vcr.stop();
		}

		void rew() {
			vcr.rew();
		}

		void ff() {
			vcr.ff();
		}
}
```

- 위처럼 Tv 클래스를 조상으로하고 VCR 클래스를 TVCR 클래스에 포함시켜서 사용함, 이렇게 해서 다중상속을 적용할 수 있음

### Object 클래스 - 모든 클래스의 조상

- Object 클래스는 모든 클래스 상속 계층도의 최상위에 있는 조상 클래스임
- 다른 클래스로부터 상속 받지 않는 모든 클래스들은 자동적으로 Object 클래스로부터 상속받게 함으로써 이것을 가능하게 함
- 그동안 Java에서 쓴 메소드들은 이것때문에 가능한 것이었음

### 2. 오버라이딩(overriding)

- 조상 클래스로부터 상속받은 메소드의 내용을 변경하는 것을 오버라이딩이라고 함
- 상속받은 메소드를 그대로 사용하기도 하지만, 자손 클래스 자신에 맞게 변경해야하는 경우 오버라이딩 한다고 함

```java
class Point {
		int x;
		int y;
		
		String getLocation() {
				return "x : " + x + ", y : "+ y;
		}
}

class Point3D extends Point {
		int z;
		
		String getLocation() { // 오버라이딩
				return "x :" + x + ", y :" + y + ", z :" + z;
		}
}
```

- 위와 같이 새로 메소드를 정의하는 것보다 기존에 있던 메소드를 오버라이딩해서 쓰는 것이 훨씬 더 나음

### 오버라이딩의 조건

- 오버라이딩은 메소드의 내용만을 새로 작성하는 것이므로 메소드의 선언부는 조상의 것과 완전히 일치해야함
- 자손 클래스에서 오버라이딩하는 메소드는 조상 클래스의 메소드와 이름이 같아야 하고 매개변수가 같아야 하며 반환타입이 같아야 함 즉, 선언부가 서로 일치해야함
- 단, 접근 제어자와 예외는 제한된 조건 하에서만 다르게 변경할 수 있음
- 접근 제어자는 조상 클래스의 메서드보다 좁은 범위로 변경 할 수 없음
    - 예를 들어 조상 클래스가 portected로 정의되어 있으면 오버라이딩 할 경우 메서드는 protected나 public이어야 함, 대부분 같은 범위의 접근 제어자를 사용함
    - 넓은 곳에서 좁은 순으로 나열하면 : public, protected, (default), private임
- 조상 클래스의 메소드보다 많은 수의 예외를 선언할 수 없다
    - 예외의 개수가 적은 것 말고도 만일 오버라이딩 했을 때 Exception으로 선언했으면 이는 모든 예외의 최고 조상이므로 이 역시 예외를 조상보다 더 선언하게 된 것이다
- 인스턴스 메서드를 static 메서드로 또는 그 반대로 변경할 수 없다

### 오버로딩 vs. 오버라이딩

- 오버로딩은 기존에 없는 새로운 메서드를 추가하는 것이고(new)
- 오버라이딩은 조상으로부터 상속받은 메서드의 내용을 변경하는 것이다(change, modify)

### Super

- 자손 클래스에서 조상 클래스로부터 상속받은 멤버를 참조하는데 사용되는 참조 변수임
- 멤버변수와 지역변수의 이름이 같을 때 this를 붙인것과 같은 로직

```java
class SuperTest {
	public static void main(String args[]) {
			Child c = new Child();
			c.method();
	}
}

class Parent {
		int x=10;
}

class Child extends Parent {
		int x=20;
	
		void method() {
			System.out.println("x=" + x); // 20
			System.out.println("this.x=" + this.x); // 20
			System.out.println("super.x=" + super.x); // 10
		}
}
```

- 메소드 역시 super를 써서 호출할 수 있음, super로 호출한뒤 추가적으로 작업을 덧붙임, 이러면 조상클래스가 변경되도 자연스럽게 반영됨

```java
class Point { 
		int x;
		int y;

		String getLocation() {
					return "x :" + x + ", y :" + y;
		}
}

class Point3D extends Point {
		int z;
		String getLocation() { // 오버라이딩
			// return "x :" + x + ", y :" + y + ", z :" + z;
			return super.getLocation() + ", z :" + z; // 조상 메소드 호출
		}
}
```

### Super() - 조상 클래스의 생성자

- 조상 클래스의 생성자를 호출하는데 사용됨
- 자손 클래스의 인스턴스를 생성하면, 자손의 멤버와 조상의 멤버가 모두 합쳐진 하나의 인스턴스가 생성됨, 이때 조상 클래스 멤버의 초기화 작업이 수행되어야 하기 때문에 자손 클래스의 생성자에서 조상 클래스의 생성자가 호출되어야 함
- Object 클래스를 제외한 모든 클래스의 생성자 첫 줄에 생성자, this() 또는 super(),를 호출해야함, 그렇지 않으면 컴파일러가 자동적으로 super();를 생성자의 첫줄에 삽입함

```java
class PointTest {
	public static void main(Strin args[]) {
			Point3D p3 = new Point3D(1,2,3);
	}
}

class Point {
		int x, y;
		
		Point(int x, int y) {
			this.x = x;
			this.y = y;
		}

		String getLocation() {
			return "x :" + x + ", y :" + y;
		}
}

class Point3D extends Point {
		int z;

		Point3D(int x, int y, int z) {
			super(x, y); // 조상클래스의 생성자 Point(int x, int y)를 호출함
			this.z = z;
		}
		
		String getLocation() { // 오버라이딩
			return "x :" + x + ", y :" + y + ", z :" + z;
		}
}		
```

- 위와 같이 Point() 생성자를 호출하여 정의해주어야 한다. 즉, 조상 클래스의 멤버변수는 이처럼 조상의 생성자에 의해 초기화되도록 해야함

### 3.package와 import

### 패키지

- 패키지란 클래스의 묶음이다, 서로 관련된 클래스들끼리 그룹 단위로 묶어 놓은 것임
- 클래스가 물리적으로 하나의 클래스파일(.class)인 것과 같이 패키지는 물리적으로 하나의 디렉토리임
- 예를 들어 String 클래스도 java.lang 패키지에 속함
- 하나의 소스파일에는 첫 번째 문장으로 단 한 번의 패키지 선언만을 허용함
- 모든 클래스는 반드시 하나의 패키지에 속해야함
- 패키지는 점(.)을 구분자로 하여 계층구조로 구성할 수 있음
- 패키지는 물리적으로 클래스 파일(.class)을 포함하는 하나의 디렉토리임

### 패키지 선언

- 패키지 선언은 소스파일 맨 위에 한 줄만 적어주면 됨

```java
package com.codechobo.book;

class PackageTest {
		public static void main(String[] args) {
				System.out.println("Hello World!");
		}
}
```

### import문

- 다른 패키지의 클래스를 사용하려면 패키지 명이 포함된 클래스 이름을 사용해야함
- import문의 역할은 컴파일러에게 소스파일에 사용된 클래스의 패키지에 대한 정보를 제공하는 것임

```java
import java.util.Calendar;
import java.util.Date;

// 한 번에 처리
import java.util.*;
```

- java.lang의 경우는 자동으로 처리되어 있음

### static import문

- static import문을 사용하면 static 멤버를 호출할 때 클래스 이름을 생략할 수 있음

```java
import static java.lang.System.out;
import static java.lang.Math.random;

// System.out을 out만으로 참조가능

out.println(random());
```

### 4.제어자(modifier)

- 접근제어자
- public, protected, default, private
- 그 외
- static, final, abstract, native, transient, synchronized, volatile, strictfp

### static - 클래스의, 공통적인

- 클래스변수(static 멤버변수)는 인스턴스에 관계없이 같은 값을 가짐, 하나의 변수를 모든 인스턴스가 공유함
- 인스턴스를 생성하지 않고 사용 가능함
- static이 사용될 수 있는 곳 - 멤버변수, 메서드, 초기화 블럭
- static 멤버변수
    - 모든 인스턴스에 공통적으로 사용되는 클래스변수가 됨
    - 클래스 변수는 인스턴스를 생성하지 않고도 사용 가능함
    - 클래스가 메모리에 로드될 때 생성됨
- static 메서드
    - 인스턴스를 생성하지 않고도 호출이 가능한 static 메서드가 됨
    - static메서드 내에서는 인스턴스멤버들을 직접 사용할 수 없음
- 인스턴스를 생성하지 않고도 호출이 가능해서 편리하고 속도가 빠름

### final - 마지막의, 변경될 수 없는

- 변수에 사용되면 값을 변경할 수 없는 상수가 되며, 메서드에 사용되면 오버라이딩을 할 수 없게 되고 클래스에 사용되면 자신을 확장하는 자손 클래스에 정의하지 못함
- final 클래스
    - 변경될 수 없는 클래스, 확장될 수 없는 클래스가 됨
    - 그래서 final로 지정된 클래스는 다른 클래스의 조상이 될 수 없음
- final 메서드
    - 변경될 수 없는 메서드, final로 지정된 메서드는 오버라이딩을 통해 재정의 될 수 없음
- final 멤버변수, 지역변수
    - 변수 앞에 final을 붙이면, 값을 변경할 수 없는 상수가 됨
- 일반적으로 선언과 초기화를 동시에 하지만 인스턴스변수의 경우 생성자에서 초기화 되도록 할 수 있음
- 클래스내에 매개변수를 갖는 생성자를 선언하여, 인스턴스를 생성할 때 final이 붙은 멤버변수를 초기화하는데 필요한 값을 생성자의 매개변수로부터 제공받는 것임

### abstract - 추상의, 미완성의

- 메서드의 선언부만 작성하고 실제 수행내용은 구현하지 않은 추상 메서드를 선언하는데 사용됨
- abstract 클래스
    - 클래스 내에 추상 메서드가 선언되어 있음을 의미함
- abstract 메서드
    - 선언부만 작성하고 구현부는 작성하지 않은 추상 메서드임을 알림
- 추상 클래스는 인스턴스를 생성할 수 없다, 하지만 이 클래스를 상속받아 원하는 메서드만 오버라이딩해도 된다는 장점이 있음

### 접근 제어자

- 멤버 또는 클래스에 사용되어, 해당하는 멤버 또는 클래스를 외부에서 접근하지 못하도록 제한하는 역할을 함
- 실제로 되어 있지 않지만 default가 되어 있음
- 접근 제어자가 사용될 수 있는 곳 - 클래스, 멤버변수, 메서드, 생성자
- private - 같은 클래스 내에서만 접근이 가능함
- default - 같은 패키지 내에서만 접근이 가능함
- protected - 같은 패키지 내에서 그리고 다른 패키지의 자손클래스에서 접근이 가능함
- public - 접근 제한이 없음
- protected의 경우 상속관계에 있는 자손클래스에서 접근하는 것을 의미함
- 접근 제어자를 사용하는 이유
- 외부로부터 데이터를 보호하기 위해서
- 외부에는 불필요한, 내부적으로만 사용되는, 부분을 감추기 위해서
- 적절한 접근 제어자를 써서 그 범위를 확인하고 이를 바탕으로 불필요한 누출을 막는것이 주된 목적임
- 생성자의 접근 제어자를 private 처리해서 외부에서 생성자에 접근할 수 없도록 할 수 있게함 하지만 이는 인스턴스를 생성해서 반환해주는 부분을 public 메서드로 제공해서 이 클래스의 인스턴스는 사용할 수 있도록 해줘야한다, 이러면 인스턴스의 개수를 제한할 수 있다

```java
final class Singleton {
		private static Singleton s = new Singleton();
	
		private Singleton() {
			//...
		}

		public static Singleton getInstance() {
				if(s==null)
						s = new Singleton();
				return s;
		}
}

class SingletonTest {
	public static void main(String args[]) {
		// Singleton s = new Singleton(); -> 에러 발생함!
				Singleton s = Singleton.getInstance();
	}
}
```

### 제어자(modifier)의 조합

- 클래스 → public, (default), final, abstract
- 메서드 → 모든 접근 제어자, final, abstract, static
- 멤버변수 → 모든 접근 제어자, final, static
- 지역변수 → final
- 제어자를 조합해서 사용할 때 주의해야 할 사항
- 메서드에 static과 abstract를 함께 사용할 수 없음 → static 메서드는 몸통이 있는 메서드에만 사용할 수 있음
- 클래스에 abstract와 final을 동시에 사용할 수 없음 → 클래스에 사용되는 final은 클래스를 확장할 수 없다는 의미이고 abstract는 상속을 통해서 완성되어야 한다는 의미이므로 서로 모순됨
- abstract메서드의 접근 제어자가 private일 수 없음 → abstract메서드는 자손클래스에서 구현해주어야 하는데 접근 제어자가 private이면, 자손클래스에서 접근할 수 없음
- 메서드에 private과 final을 같이 사용할 필요는 없음 → 접근 제어자가 private인 메서드는 오버라이딩 할 수 없기 때문임, 이 둘 중 하나만 사용해도 의미가 충분함

### 5.다형성(Polymorphism)

- 여러가지 형태를 가질 수 있는 능력, 자바에서는 한 타입의 참조변수로 여러 타입의 객체를 참조할 수 있도록 함으로써 다형성을 구현함
- 즉 조상클래스 타입의 참조변수로 자손 클래스의 인스턴스를 참조할 수 있도록 한 것
- 서로 상속관계에 있다면 조상 클래스 타입의 참조 변수로 자손 클래스의 인스턴스를 참조하도록 하는 것도 가능함
- `Tv t = new CaptionTv();`
- 여기서 CaptionTv 인스턴스의 모든 멤버를 사용할 수 없다, 즉 CaptionTv 클래스에 저의된 변수나 메소드 사용이 불가함
- 이와 반대로 `CaptionTv c = new Tv();` 는 불가능하다, Tv의 멤버 개수가 CaptionTv의 멤버가 더 많기 때문이다
- 즉 정리하면 참조변수가 사용할 수 있는 멤버의 개수는 인스턴스의 멤버 개수보다 같거나 적어야함
- 결론적으로 조상타입의 참조변수로 자손타입의 인스턴스를 참조할 수 있지만 반대로 자손타입의 참조변수로 조상타입의 인스턴스를 참조할 수는 없음

### 참조변수의 형변환

- 서로 상속관계에 있다면 클래스사이에서 형변환이 가능함
- 자손타입 → 조상타입(Up-casting) : 형변환 생략가능
- 자손타입 ← 조상타입(Down-casting) : 형변환 생략불가
- Car 클래스는 FireEngine 클래스와 Ambulance 클래스의 조상임

```java
Car car = null;
FireEngine fe = new FireEngine();
FireEngine fe2 = null;

car = fe; // car = (Car)fe;에서 형변환 생략됨, 업캐스팅
fe2 = (FireEngine)car; // 형변환 생략불가, 다운캐스팅
```

- 참조변수의 형변환을 통해서, 참조하고 있는 인스턴스에서 사용할 수 있는 멤버의 범위(개수)를 조절하는 것

### instanceof연산자

- 참조변수가 참조하고 있는 인스턴스의 실제 타입을 알아보기 위해 사용함
- 어떤 타입에 대한 instanceof 연산의 결과가 true라는 것은 검사한 타입으로 형변환이 가능하다는 것을 뜻함

### 참조변수와 인스턴스의 연결

- 멤버변수가 조상 클래스와 자손 클래스에 중복으로 정의된 경우, 조상타입의 참조변수를 사용했을 때는 조상 클래스에 선언된 멤버변수가 사용되고, 자손타입의 참조변수를 사용했을 때는 자손 클래스에 선언된 멤버변수가 사용됨
- 메서드의 경우 참조변수의 타입에 관계없이 항상 실제 인스턴스의 타입인 해당 클래스에 정의된 메소드가 호출됨

```java
class BindingTest {
	public static void main(String[] args) {
			Parent p = new Child();
			Child  c = new Child();

			System.out.println("p.x = " + p.x); // p.x = 100
			p.method(); // Child Method
		
			System.out.println("c.x = " + c.x); // c.x = 200
			c.method(); // Child Method
	}
}

class Parent {
	 int x = 100;

	 void method() {
			System.out.println("Parent Method");
	 }
}

class Child extends Parent {
	 int x = 200;

	 void method() {
			System.out.println("Child Method");
	 }
}
```

### 매개변수의 다형성

- 매개변수의 참조변수를 넘겨주어서 이를 활용하여 독립된 메소드에 넘겨서 활용할 수 있다
- 아래와 같이 여러개의 클래스를 만들고 상속에 얽혀있는 것인데 이를 다형성을 활용하여 쉽게 처리하고 정리할 수 있다

```java
class Product {
	int price; // 제품의 가격
	int bonusPoint; // 제품구매 시 제공하는 보너스 점수

	Product(int price) {
		this.price = price;
		bonusPoint = (int)(price/10.0); // 보너스점수는 제품가격의 10%
	}
}

class Tv extends Product {
	Tv() {
		// 조상클래스의 생성자 Product(int price)를 호출함
		super(100); // Tv의 가격을 100만원으로 만듬
	}
	// Object 클래스의 toString()을 오버라이딩함
	public String toString() { return "Tv"; }
}

class Computer extends Product {
	Computer() { super(200); }
	
	public String toString() { return "Computer"; }
}

class Buyer { // 고객, 물건을 사는 사람
	int money = 1000; // 소유금액
	int bonusPoint = 0; // 보너스 점수

	void buy(Product p) {
		if(money < p.price) {
				System.out.println("잔액이 부족하여 물건을 살 수 없습니다.");
				return;
		}

		money -= p.price; // 가진 돈에서 구입한 제품의 가격을 뺌
		bonusPoint += p.bonusPoint; // 제품의 보너스 점수를 추가함
		System.out.println(p + "을/를 구입하셨습니다.");
	}
}

class PolyArgumentTest {
	public static void main(String args[]) {
		Buyer b = new Buyer();
		
		b.buy(new Tv());
		b.buy(new Computer());
	
		System.out.println("현재 남은 돈은 " + b.money + "만원입니다.");
		System.out.println("현재 보너스점수는 " + b.bonusPoint + "점입니다.");
	}
}
```

### 여러 종류의 객체를 배열로 다루기

- 위처럼 클래스에 대해서 객체를 참조변수로 활용하고 객체를 참조하는 것이 가능한데, 이를 배열로 묶어서 담을 수 있음
- 즉 공통의 조상을 가진 서로 다른 종류의 객체를 배열로 묶는 것 혹은 묶어서 다루고싶은 객체들의 상속관계를 따져서 가장 가까운 공통조상 클래스 타입의 참조변수 배열을 생성해서 객체들을 저장함
- 동적을 관리하기 위해서 Vector 클래스를 사용함(주로 근데 ArrayList)를 많이씀

### 6.추상클래스

- 추상클래스는 미완성 설계도라고 할 수 있음, 미완성 메서드를 포함하고 있다는 의미임
- 인스턴스를 생성할 수 없고 상속을 통해서 자손클래스에 의해서만 완성될 수 있음
- 새로운 클래스를 작성하는데 있어서 바탕이 되는 조상클래스로서 중요한 의미를 가짐
- 어느정도 틀을 갖춘 상태에서 시작

### 추상 메서드

- 메서드의 선언부만 작성하고 구현부는 작성하지 않은 것, 실제 수행될 내용을 작성하지 않은 것을 의미함
- 이는 메서드의 내용이 상속받는 클래스에 따라 달라질 수 있기 때문에 조상 클래스에서는 선언부만을 작성하고, 주석을 덧붙여 어떤 기능을 수행할 목적으로 작성되었는지 알려주고, 실제 내용은 상속받는 클래스에서 구현하도록 비워두는 것임
- 이를 오버라이딩하여 조상인 추상 클래스의 추상 메서드를 모두 구현해주어야 함
- 만일 조상으로부터 상속받은 추상 메소드 중 하나라도 구현하지 않는다면 자손 클래스 역시 추상 클래스로 지정해주어야 함

### 추상클래스의 작성

- 추상화는 기존의 클래스의 공통부분을 뽑아서 조상 클래스를 만드는 것임
- 구체화는 상속을 통해 클래스를 구현, 확장하는 작업임
- 즉 서로 반대되는 개념으로 생각하고 이해하면 됨

### 7.인터페이스

- 인터페이스는 일종의 추상클래스임, 하지만 일반 메서드 또는 멤버변수를 가질 수 없음
- 구현된 아무것도 없고 밑그림만 그려져 있는 기본 설계도임
- 다른 클래스를 작성하는데 도움을 줄 목적으로 작성됨

### 인터페이스 작성

- 모든 멤버변수는 `public static final` 이어야 하며, 생략할 수 있음
- 모든 메서드는 `public abstract` 여야 하며, 생략할 수 있음
- 제어자가 생략되어도 컴파일러가 알아서 추가해줌

### 인터페이스의 상속

- 인터페이스는 인터페이스로부터만 상속 받을 수 있고, 다중 상속, 여러 개의 인터페이스로부터 상속 받는 것이 가능함

### 인터페이스의 구현

- 그 자체로는 인스턴스를 생성할 수 없고, 자신에 정의된 추상메서드의 몸통을 만들어주는 클래스를 작성해줘야함
- 하지만 extends 키워드가 아닌 구현한다는 의미의 implements를 사용함
- 만일 구현하는 인터페이스의 메서드 중 일부만 구현한다면, abstract를 붙여서 추상클래스로 선언해야함
- 상속과 구현을 동시에 할 수 있음

```java
class FighterTest {
	public static void main(String[] args) {
		Fighter f = new Fighter();
		
		if (f instanceof Unit)
				System.out.println("f는 Unit클래스의 자손입니다");
		if (f instanceof Fightable)
				System.out.println("f는 Fightable인터페이스를 구현했습니다");
		if (f instanceof Movable)
				System.out.println("f는 Movable인터페이스를 구현했습니다.");
		if (f instanceof Attackable)
				System.out.println("f는 Attackable인터페이스를 구현했습니다.");
		if (f instanceof Object)
				System.out.println("f는 Object클래스의 자손입니다.");
	}
}

class Fighter extends Unit implements Fightable {
	public void move(int x, int y) { /*내용 생략*/ }
	public void attack(Unit u) { /*내용 생략*/ }
}

class Unit {
		int currentHP; // 유닛의 체력
		int x; // 유닛의 위치(x좌표)
		int y; // 유닛의 위치(y좌표)
}

interface Fightable extends Movable, Attackable { }
interface Movable { void move(int x,int y); }
interface Attackable { void attack(Unit u); }
```

- Fighter 클래스는 Unit클래스로부터 상속받고 Fightable 인터페이스만을 구현함
- Unit 클래스는 Object 클래스의 자손이고, Fightable 인터페이스는 Attackable과 Movable 인터페이스의 자손이므로 Fighter 클래스는 이 모든 클래스와 인터페이스의 자손임
- 인터페이스에서 제어자가 생략되어 있는 것인데 그러므로 구현할 때 public으로 제어자를 해줘야함

### 인터페이스를 이용한 다중상속

- 두 조상으로부터 상속받는 멤버 중에서 멤버변수의 이름이 같거나 메서드의 선언부가 일치하고 구현 내용이 다르면 이 두 조상으로부터 상속받는 자손 클래스는 어느 조상의 것을 상속받게 되는 것인지 알 수없음, 그래서 다중상속을 하지 않는 것임
- 인터페이스는 다중상속을 위한 것이 본질적으로 아님
- 인터페이스는 static 상수만 정의할 수 있어 조상클래스의 멤버변수와 충돌하는 경우는 거의 없고 구분이 가능함, 그리고 추상 메서드도 구현 내용이 전혀 없어 메서드와 선언부가 일치패도 조상 클래스 쪽 메서드를 상속받으면 되므로 문제가 되지 않음
- 이렇게 하면 다중상속의 장점을 잃어버리는데, 이를 해결하기 위해서 두 조상클래스 중 비중이 높은쪽을 선택해 다른 한쪽은 클래스 내부에 멤버로 포함시키는 방식을 하거나 필요한 부분만 뽑아서 인터페이스로 만들 수 있음

```java
public class Tv {
		protected boolean power;
		protected int channel;
		protected int volume;

		public void power() { power = !power; }
		public void channelUp() { channel++; }
		public void channelDown() { channel--; }
		public void volumeUp() { volume++; }
		public void volumeDown() { volume--; }
}
```

```java
public class VCR {
		protected int counter; // VCR의 카운터

		public void play() {
			// Tape 재생		
		}
		
		public void stop() {
			// 재생 멈춤
		}
		
		public void reset() {
			counter = 0;
		}
		
		public int getCounter() {
			return counter;
		}
	
		public void setCounter(int c) {
			counter = c;
		}
}
```

```java
// VCR 클래스에 정의된 메서드와 일치하는 추상메서드 갖는 인터페이스 작성
public interface IVCR {
		public void play();
		public void stop();
		public void reset();
		public int getCounter();
		public void setCounter(int c);
} 
```

```java
public class TVCR extends Tv implements IVCR {
		VCR vcr = new VCR();
		
		public void play() {
			vcr.play();
		}

		public void stop() {
			vcr.stop();
		}
		
		public void reset() {
			vcr.reset();
		}
		
		public int getCounter() {
			return vcr.getCounter();
		}

		public void setCounter(int c) {
			vcr.setCounter(c);
		}
}
```

- 위처럼 다중상속이 되지 않으니깐 IVCR이라는 인터페이스를 구현해서 VCR클래스의 인스턴스를 활용해서 구현할 수 있음
- VCR 클래스 내용이 변경되어도 자동적으로 반영이 가능하다
- 인터페이스를 통해서 다형적 특성을 이용할 수 있다는 장점이 있음

### 인터페이스를 이용한 다형성

- 자손클래스의 인스턴스를 조상타입의 참조변수로 참조하는 것이 가능한 것이 인터페이스에서도 가능함
- 형변환도 가능함

```java
Fightable f = (Fightable)new Fighter();

Fightable f = new Fighter();
```

- 리턴타입이 인터페이스라는 것은 메서드가 해당 인터페이스를 구현한 클래스의 인스턴스를 반환한다는 것을 의미함
- 분산환경 프로그래밍에서 매우 유용함, 서버측 변경으로 새로 개정된 프로그램 활용이 가능함

```java
interface Parseable {
	// 구문 분석작업을 수행함
	public abstract void parse(String fileName);
}

class ParserManager {
	// 리턴타입이 Parseable 인터페이스임
	public static Parseable getParser(String type) {
			if(type.equals("XML")) {
					return new XMLParser();
			} else {
					Parseable p = new HTMLParser();
					return p;
					// return new HTMLParser();
			}
	}
}

class XMLParser implements Parseable {
	public void parse(String fileName) {
		/* 구문 분석작업을 수행하는 코드를 적음 */
		System.out.println(fileName + "- XML parsing completed.");
	}
}

class HTMLParser implements Parseable {
	public void parse(String fileName) {
		/* 구문 분석작업을 수행하는 코드를 적음 */
		System.out.println(fileName + "-HTML parsing completed.");
	}
}

class ParserTest {
	public static void main(String args[]) {
		Parseable parser = ParserManager.getParser("XML");
		parser.parse("document.xml");
		parser = ParserManager.getParser("HTML");
		parser.parse("document2.html");
	}
}

```

### 인터페이스의 장점

- 개발시간을 단축시킬 수 있음
    - 인터페이스가 작성되면 이를 사용해서 프로그램을 작성하는 것이 가능함, 메서드의 내용에 관계없이 선언부만 알면 되기 때문에
    - 그리고 다른 한 쪽에서 인터페이스를 구현하는 클래스를 작성하게 하면, 인터페이스를 구현하는 클래스가 작성될 때까지 기다리지 않고도 양쪽에서 동시에 개발을 진행할 수 있음
- 표준화가 가능함
    - 프로젝트에 사용되는 기본 틀을 인터페이스로 작성한 다음, 개발자들에게 인터페이스를 구현하여 프로그램을 작성하도록 함으로써 보다 일관되고 정형화된 프로그램의 개발이 가능함
- 서로 관계없는 클래스들에게 관계를 맺어 줄 수 있음
    - 서로 아무런 관계도 없는 클래스들에게 하나의 인터페이스를 공통적으로 구현하도록 함으로써 관계를 맺어 줄 수 있음
- 독립적인 프로그래밍이 가능함
    - 인터페이스를 이용하면 클래스의 선언과 구현을 분리시킬 수 있기 때문에 실제구현에 독립적인 프로그램을 작성하는 것이 가능함
    - 클래스와 클래스간의 직접적인 관계를 인터페이스를 이용해서 간접적인 관계로 변경하면 한 클래스의 변경이 관련된 다른 클래스에 영향을 미치지 않는 독립적인 프로그래밍이 가능함

```java
class RepairableTest {
	public static void main(String[] args) {
		Tank tank = new Tank();
		Dropship dropship = new Dropship();
		
		Marine marine = new Marine();
		SCV scv = new SCV();

		scv.repair(tank);
		scv.repair(dropship);
//		scv.repair(marine) // 에러 -> repair(Repairable) in SCV cannot be applied to Marine
		}
}

interface Repairable {}

class Unit {
		int hitPoint;
		final int MAX_HP;
		Unit(int hp) {
			MAX_HP = hp;
		}
		//...
}

class GroundUnit extends Unit {
	GroundUnit(int hp) {
		super(hp);
	}
}

class AirUnit extends Unit {
	AirUnit(int hp) {
		super(hp);
	}
}

class Tank extends GroundUnit implements Repairable {
	Tank() {
		super(150); // Tank의 HP는 150임
		hitPoint = MAX_HP;
	}

	public String toString() {
		return "Tank";
	}
	//...
}

class Dropship extends AirUnit implements Repairable {
	Dropship() {
		super(125); // Dropship의 HP는 125임
		hitPoint = MAX_HP;
	}

	public String toString() {
		return "Dropship";
	}
	//...
}

class Marine extends GroundUnit {
	Marine() {
		super(40);
		hitPoint = MAX_HP;
	}
	//...
}

class SCV extends GroundUnit implements Repairable {
	SCV() {
		super(60):
		hitPoint = MAX_HP;
	}

	void repair(Repairable r) {
		if (r instanceof Unit) {
				Unit u = (Unit)r;
				while(u.hitPoint!=u.MAX_HP) {
					/*Unit의 HP를 증가시킴 */
					u.hitPoint++;
				}
				System.out.println( u.toString() + "의 수리가 끝났습니다.");
		}
	}
	// ...
}

```

- 위처럼 매개변수로 Repairable 인터페이스를 넘겨 받아 repair 메서드에 의해서 수리가 가능하도록 구현을 함, 그러면 Repairable에 정의된 멤버만 사용할 수 있게됨

### 인터페이스의 이해

- 인터페이스를 이해하는데 2가지 사항이 있음
- 클래스를 사용하는 쪽(User)과 클래스를 제공하는 쪽(Provider)가 있음
- 메서드를 사용(호출)하는 쪽(User)에서는 사용하려는 메서드(Provider)의 선언부만 알면 됨(내용은 몰라도 됨)
- 위의 User와 Provider 관계에 대해서 인터페이스를 이용해서 관계를 간접적으로 변경할 수 있다
- 그러므로 직접적인 영향을 받지 않고 크게 신경쓰고 건드릴 필요가 없어지게 된다

### 디폴트 메서드와 static 메서드

- static 메서드는 인스턴스와 관계가 없는 독립적인 메서드이다
- 하지만 인터페이스의 모든 메서드는 추상 메서드이어야 한다는 규칙에 예외를 두지 않기 위해서 인터페이스와 관련된 static 메서드는 별도의 클래스에 따로 두었다
- 인터페이스에 메서드를 추가하는 것은 추상 메서드를 추가하는 것이고 이는 이 인터페이스를 구현한 기존의 모든 클래스들이 새로 추가된 메서드를 구현해야하는 일이 나타난다
- 이를 해결하기 위해 디폴트 메서드를 고안해냈는데, 디폴트 메서드는 추상 메서드의 기본적인 구현을 제공하는 메서드로 추상메서드가 아니므로, 디폴트 메서드가 새로 추가되어도 해당 인터페이스를 구현한 클래스를 변경하지 않아도 됨, 일반 메서드처럼 몸통이 있어야함
- 단, 새로 추가된 디폴트 메서드가 기존의 메서드와 이름이 중복되어 충돌하는 경우가 발생하는데 이를 해결하기 위한 대책이 있다
- 여러 인터페이스의 디폴트 메서드 간의 충돌 → 인터페이스를 구현한 클래스에서 디폴트 메서드를 오버라이딩해야 함
- 디폴트 메서드와 조상 클래스의 메서드 간의 충돌 → 조상 클래스의 메서드가 상속되고, 디폴트 메서드는 무시됨
- 필요한 쪽의 메서드와 같은 내용으로 오버라이딩하면 그만임

### 8.내부 클래스

- 내부 클래스는 클래스 내에 선언된다는 점을 제외하고는 일반적인 클래스와 다르지 않음
- 두 클래스가 서로 긴밀한 관계에 있기 때문에 선언한 것, 두 클래스의 멤버들 간에 서로 쉽게 접근할 수 있다는 장점과 외부에는 불필요한 클래스를 감춤으로써 코드의 복잡성을 줄일 수 있음

### 내부 클래스의 종류와 특징

- 변수를 선언하는 것과 같은 위치에 선언할 수 있음, 선언위치에 따라 구분됨
- 인스턴스 클래스(instance class)
    - 외부 클래스의 멤버변수 선언위치에 선언하며, 외부 클래스의 인스턴스 멤버처럼 다루어짐, 주로 외부 클래스의 인스턴스멤버들과 관련된 작업에 사용될 목적으로 선언됨
- 스태틱 클래스(static class)
    - 외부 클래스의 멤버벼수 선언위치에 선언하며, 외부 클래스의 static 멤버처럼 다루어짐, 주로 외부 클래스의 static 멤버, 특히 static 메서드에서 사용될 목적으로 선언됨
- 지역 클래스(local class)
    - 외부 클래스의 메서드나 초기화 블럭 안에 선언하며, 선언된 영역 내부에서만 사용될 수 있음
- 익명 클래스(anonymous class)
    - 클래스의 선언과 객체의 생성을 동시에 하는 이름없는 클래스(일회용)

### 내부 클래스의 선언

```java
class Outer {
		int iv = 0;
		static int cv = 0;
		
		void myMethod() {
			int lv = 0;
		}
}
```

```java
class Outer {
	class InstanceInner {}
	static class StaticInner {}

	void myMethod() {
		class LocalInner {}
	}
}
```

### 내부 클래스의 제어자와 접근성

- 내부 클래스 역시 멤버변수와 같은 위치에 선언되면 멤버변수와 같은 성질을 가짐
- 인스턴스 멤버와 static 멤버 간의 규칙이 내부 클래스에도 똑같이 적용됨
- 제어자 및 접근 제어자 사용도 가능함

### 익명 클래스(anonymous class)

- 내부 클래스들과 달리 이름이 없음, 클래스의 선언과 객체의 생성을 동시에 하기 때문에 단 한번만 사용될 수 있고 오직 하나의 객체만을 생성할 수 있는 일회용 클래스임
- 생성자도 가질 수 없고, 단 하나의 클래스를 상속받거나 단 하나의 인터페이스만을 구현할 수 있음

```java
class InnerEx6 {
	Object iv = new Object(){ void method(){} }; // 익명 클래스
	static Object cv = new Object(){ void method(){} }; // 익명 클래스

	void myMethod() {
		Object lv = new Object(){ void method(){} }; // 익명 클래스
	}
}
```