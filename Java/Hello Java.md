### 기본
- 기본

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```

`public` → 접근 제어자 public은 어디에서나 접근 가능함

`class HelloWorld` → HelloWorld라는 클래스 정의

`main` → 클래스 안에 정의된 함수, 메소드(함수) 이름, 프로그램 실행시 Java가 메인 메소드를 찾아서 실행시킴

`String[] args` → 파라미터, args라는 문자열 배열을 받음, main 메소드에게 파라미터를 전달해주면 main 메소드 안에서 args라는 이름으로 받아서 사용할 수 있음

`void main` → 메소드 함수의 리턴 값의 자료형, void일 경우 리턴 값이 없음, 돌려줄 값이 있다면 void 대신 숫자를 돌려준다면 int를 씀

`static` → 그 부분을 바로 실행 가능하게 해 줌

`System.out.println("Hello World!");` → System이라는 클래스의 out이라는 변수의 println이라는 메소드 호출함, 파라미터로 문자열 Hello World를 넘겨주면 콘솔에 출력함