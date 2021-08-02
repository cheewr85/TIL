### Scope Function(apply, with, let, also, run)
- 람다식을 호출해서 하면 일시적으로 범위가 형성이 되고 범위에서 수신객체 등의 자유롭게 접근 가능
- 어떤 것을 하기 위해서 한 것인지 알 수 있게함

![one](/img/Android/android/Kotlin/one.png)

- Apply 함수
- 블록 내부에서 객체의 프로퍼티에 접근할 수 있음, 반환값이 객체 자신이 됨, 주로 객체를 초기화할 때 사용함
```kotlin
// Kotlin
// Java에서 사용한 setter, 생성자를 활용한 초기화를 apply를 통해서
// 알아서 Person 객체를 생성하고 객체를 초기화함
val person = Person().apply {
	firstName = "Fast"
	lastName = "Campus"
}
```
```java
// Java
// 생성자에서 초기화 혹은 프로퍼티에 직접 접근해서 초기화
// 아니면 setter를 통해서 초기화
Person person = new Person();
person.firstName = "Fast";
person.lastName = "Campus";
```

- Also 함수
- 객체가 파라미터로 전달됨, 람다의 입력값으로 내려옴, 람다의 입력값은 it으로 내려옴, 하지만 직접 명시할 수 있음, 객체 유효성 디버깅 용도로 활용
```kotlin
Random.nextInt(100).also {
				print("getRandomInt() generated value $it)
}
```
```kotlin
Random.nextInt(100).also { value ->
				print("getRandomInt() generated value $value)
}
```
```java
int value = Random().nextInt(100);
System.out.print(value);
```

- let 함수
- 주로 null이 아닌 객체에서 람다를 실행할 때 사용됨, 코드 블록의 수행결과가 반환이 됨, 주로 람다를 실행할 때 사용됨
- ?.let을 쓰면 null이 아닌 값만 들어옴
```kotlin
val number: Int?

val sumNumberStr = number?.let {
	"${sum(10,it)}"
}
```
```kotlin
Integer number = null;
String sumNumberStr = null;

if (number != null) {
	sumNumberStr = "" + sum(10, number);
}
```

- orEmpty는 String이 nullable일 경우에만 사용, null인 스트링을 null이 아닌 빈값으로 바꿔줌
```kotlin
val number: Int?

val sumNumberStr = number?.let {
	"${sum(10,it)}"
}.orEmpty() 
```
```kotlin
Integer number = null;
String sumNumberStr = null;

if (number != null) {
	sumNumberStr = "" + sum(10, number);
} else {
	sumNumberStr = "";
}
```

- With 함수
- 반환값은 람다의 결과값임, 객체로도 나올 수 있음, 객체 함수, 변수들을 this로 호출 가능함
```kotlin
val person = Person()

with(person) { // person에 있는 함수를 모두 실행시키겠다는걸 의미
		work()
		sleep()
		println(age)
}
```
```java
Person person = new Person();

person.work();
person.sleep();
System.out.println(person.age);
```

- Run 함수
- 어떤 값을 계산할 필요가 있거나 객체 구성과 결과 계산이 한꺼번에 있을 때 유용함
```kotlin
val result = service.run {
		port = 8000
		query()
}
```
```java
service.port = 8000;
Result result = service.query();
```

- Data 클래스가 빌트인 되어 있음, 데이터를 저장하는 목적에 클래스 존재함
- 모델 클래스 사용할 때 주로 Data 클래스 사용함
- 람다식
- 함수에 함수를 전달하고 전달된 함수에서 함수를 실행시키는 역할
- 주로 리스너 같은것
```java
// 자바 버전, 리스너를 사용하고 직접 구현체를 구현 onClick
button.setOnClickListener(new View.OnClickListener() {
	@Override
	public void onClick(View view) {
		,,,
	}
})
```
```kotlin
// Kotlin 버전, 간결하게 표현 가능
button.setOnClickListener { v ->

}
```

- lateinit, lazy init
- Nullsafe한 코드를 사용하기 위해서 non-null Type으로 변수를 선언함, 초기화를 바로 해줘야 함
- lateinit은 non-null 한 타입만 가능, 전역변수로 선언했을 때 초기값을 바로 넣어주지 못할 때 추후 초기화가 가능함
```kotlin
var nullableNumber: Int? = null

lateinit var lateinitNumber: Int

// 추후 초기화하는 코드
lateinitNumber = 10

// 사용할 때
nullableNumber?.add()

lateinitNumber.add()
```
```kotlin
val lazyNumber :Int by lazy {
		100
}

// 사용하기 전까지는 lazyNumber라는 변수에 100이 할당되지 않음

lazyNumber.add()
// 사용할 때 100이 할당됨
```