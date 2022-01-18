### Template 패턴
- 템플릿의 기능을 가진 패턴
- 상위 클래스 쪽에 템플릿에 해당하는 메소드가 정의되어 있고, 그 메소드의 정의 안에는 추상 메소드가 사용되고 있음
- 추상 메소드를 실제로 구현하는 것은 하위 클래스임, 하위 클래스 측에서 메소드를 구현하면 구체적인 처리가 결정됨
- 서로 다른 하위 클래스가 서로 다른 구현을 실행하면 서로 다른 처리가 실행됨, 어떤 하위 클래스에서 어떤 구현을 하더라도 처리의 큰 흐름은 상위 클래스에서 결정한대로 이루어짐
- 상위 클래스에서 뼈대를 결정하고, 하위 클래스에서 그 구체적인 내용을 결정함

### 예제
![one](/img/DesignPattern/Template/one.png)

- AbstractDisplay : 메소드 display만 구현되고 있는 추상 클래스
- CharDisplay : 메소드, open, print, close를 구현하고 있는 클래스
- StringDisplay : 메소드 open, print, close를 구현하고 있는 클래스

### AbstractDisplay
```java
public abstract class AbstractDisplay { // 추상클래스 AbstractDisplay
		public abstract void open(); // 하위 클래스에 구현을 맡기는 추상 메소드(1) open
		public abstract void print(); // 하위 클래스에 구현을 맡기는 추상 메소드(2) print
		public abstract void close(); // 하위 클래스에 구현을 맡기는 추상 메소드(3) close
		public final void display() { // 추상 클래스에서 구현되고 있는 메소드 display
				open(); // 우선 open하고
				for (int i = 0; i < 5; i++) { // 5번 print를 반복하고
						print();
				}
				close(); /// 마지막으로 close함(display 메소드에서 구현되고 있는 내용)
		}
}
```
- display 메소드는 정의되어 있고 이 메소드 안에서 open, print, close 세 가지 메소드 사용함, 하지만 이 세 가지 메소드는 실체가 없음, 이 추상 메소드를 사용하고 있는 display 메소드가 템플릿 메소드임
- open, print, close는 CharDisplay, StringDisplay 같은 하위 클래스에서 실제로 메소드를 구현함, AbstractDisplay에서는 실제로 무엇을 하고 있는가를 알 수 없음, 하위 클래스에게 맡기고 있음

### CharDisplay
```java
public class CharDisplay extends AbstractDisplay {
		// CharDisplay는 AbstractDisplay의 하위 클래스
		
		private char ch; // 표시해야 할 문자
		public CharDisplay(char ch) { // 생성자에서 전달된 문자 ch를
				this.ch = ch; // 필드에 기억해둠
		}
		public void open() { // 상위 클래스에서는 추상 메소드였음
				// 여기에서 오버라이드해서 구현함
				System.out.print("<<"); // 개시 문자열 "<<"을 표시함
		}
		public void print() { // print 메소드도 여기에서 구현함
				// 이것이 display에서 반복해서 호출됨
				System.out.print(ch); // 필드에 기억해 둔 문자를 1개 표시함
		}
		public void close() { // close 메소드도 여기에서 구현함
				System.out.println(">>"); // 종료 문자열 ">>"을 표시
		}
}
```
- CharDisplay는 open, print, close가 모두 구현되어 있기 때문에 추상 클래스가 아님
- 각 구현한 메소드 역할은 아래와 같음
    - open : 문자열 “<<”을 표시함
    - print : 생성자에서 주어진 1문자를 표시함
    - close : 문자열 “>>”을 표시함

### StringDisplay
```java
public class StringDisplay extends AbstractDisplay {
		// StringDisplay도 AbstractDisplay의 하위 클래스
		private String string; // 표시해야 할 문자열
		private int width; // 바이트 단위로 계산한 문자열의 길이
		public StringDisplay(String string) {
				this.string = string; // 생성자에서 전달된 문자열 string을 필드에 기억
				this.width = string.getBytes().length; // 바이트 단위의 길이도 필드에 기억해 두고 나중에 사용함
		}
		public void open() { // 오버라이드해서 정의한 open 메소드
				printLine(); // printLine에서 선을 그림
		}
		public void print() { 
				System.out.println("|" + string + "|"); // print메소드는 필드에 기억해 둔 문자열의 전후에 "|"을 붙여서 표시
		}
		public void close() {
				printLine(); // open처럼 printLine 메소드에서 선을 그림
		}
		private void printLine() { // open과 close에서 호출된 printLine 메소드, 이 클래스 안에서만 사용 가능
				System.out.print("+"); // 테두리의 모서리를 표시하는 "+" 마크를 표시
				for (int i = 0; i < width; i++) {
						System.out.print("-"); // width개의 "-"을 표시하고 테두리 선으로 사용함
				}
				System.out.println("+"); // 테두리의 모서리를 표시하는 + 마크를 표시
		}
}
```
- 각 구현한 메소드 역할은 아래와 같음
    - open : 문자열 “+——+”을 표시함
    - print : 생성자에서 주어진 문자열을 “|”와 “|”사이에 표시함
    - close : 문자열 “+——+”을 표시함

### Main 클래스
```java
public class Main {
		public static void main(String[] args) {
				// 'H'를 가진 CharDisplay 인스턴스 1개를 만듬
				AbstractDisplay d1 = new CharDisplay('H');
				// "Hello, World."를 가진 StringDisplay의 인스턴스 1개를 만듬
				AbstractDisplay d2 = new StringDisplay("Hello, world."); 
				// "안녕하세요."를 가진 StringDisplay의 인스턴스 1개를 만듬
				AbstractDisplay d3 = new StringDisplay("안녕하세요.");
				// d1, d2, d3 모두 같은 AbstractDisplay의 하위 클래스의 인스턴스이기 때문에
				// 상속한 display 메소드 호출 가능함
				// 실제 동작은 CharDisplay, StringDisplay에서 결정
				d1.display(); 
				d2.display();
				d3.display();
		}
}
```
- d1의 경우 `<<HHHHH>>` 가 출력되고 d2, d3 경우 `+---------+` 로 위아래를 형성하고 가운데에는 각각 지정한 `|Hello, world.|` 와 `|안녕하세요.|` 가 반복 출력되는 형성을 함

### 패턴의 등장인물
![one](/img/DesignPattern/Template/two.png)

- AbstractClass(추상 클래스)의 역할
    - AbstractClass는 템플릿 메소드를 구현함, 그 템플릿 메소드에서 사용하고 있는 추상 메소드를 선언함
    - 이 추상 메소드는 하위 클래스인 ConcreteClass 역할에 의해 구현됨(예제 프로그램에서 AbstractDisplay가 그 역할을 함)
- ConcreteClass(구현 클래스)의 역할
    - AbstractClass 역할에서 정의되어 있는 추상 메소드를 구체적으로 구현함
    - 여기에서 구현한 메소드는 AbstractClass역의 템플릿 메소드에서 호출됨
    - 예제 프로그램에서 CharDisplay, StringDisplay가 그 역할을 함

## 사고력 키우기

### 로직을 공통화할 수 있다
- 상위 클래스의 템플릿 메소드에서 알고리즘이 기술되어 있으므로 하위 클래스측에서는 알고리즘을 일일이 기술할 필요가 없음
- 만약 Template Method 패턴을 사용하지 않고 복사 붙여넣기로 ConcreteClass만을 구현했다면 모두 비슷하지만 다른 클래스가 됨, 버그 수정을 위해서 모든 ConcreteClass를 수정해야 하지만 Template 메소드에 오류가 발견되면 해당 메소드만 수정하면 됨

### 상위 클래스와 하위 클래스의 연계
- 상위 클래스에서 선언된 추상 메소드를 실제로 하위 클래스에서 구현할 때에는 그 메소드가 어느 타이밍에서 호출되는지 이해해야함
- 상위 클래스의 소스 프로그램 없이 하위 클래스의 구현이 어려울 수 있음

### 하위 클래스를 상위 클래스와 동일시함
- 예제에서 CharDisplay 인스턴스도 StringDisplay 인스턴스도 AbstractDisplay형의 변수에 대입을 하고거 display 메소드를 호출함
- 상위 클래스형의 변수가 있고, 그 변수에 하위 클래스형의 인스턴스가 대입된다고 가정함
- 이때 instanceof 등으로 하위 클래스의 종류를 특정하지 않아도 프로그램이 작동하도록 만드는 게 좋음
- 상위 클래스형 변수에 하위 클래스의 어떠한 인스턴스를 대입해도 제대로 작동할 수 있도록 하는 원칙 적용

## 보강 : 클래스 계층과 추상 클래스

### 상위 클래스에서 하위 클래스에게 요청
- 클래스 계층을 생각하면 대부분 하위 클래스의 시점에서 생각을 함
    - 상위 클래스에서 정의되어 있는 메소드를 하위 클래스에서 이용할 수 있음
    - 하위 클래스에 약간의 메소드를 기술해서 새로운 기능을 추가할 수 있음
    - 하위 클래스에서 메소드를 오버라이드하면 동작을 변경할 수 있음
- 여기서 조금 시점을 바꾸어 상위 클래스의 입장에서 생각해 볼 수 있음
- 상위 클래스에서 추상 메소드가 선언되어 있다고 가정하면 메소드의 구현은 당연히 하위 클래스에 맡겨져 있음
- 추상 메소드를 선언한다는 것은 프로그램을 사용해서 아래와 같은 주장을 하는 것
    - 하위 클래스에서 메소드가 구현되길 원함
    - 하위 클래스에 대해서 그 메소드의 구현을 요청함
- 하위 클래스는 상위 클래스에서 선언된 추상 메소드를 구현할 책임이 생겼다고 말할 수 있음

### 추상 클래스의 의의
- 추상 클래스는 인스턴스를 만들 수 없음, 이때 무슨 도움이 될까 생각을 할 수 있음
- 추상 메소드에는 메소드의 본체가 기술되어 있지 않기 때문에 구체적인 처리 내용을 알 수 없음, 그러나 메소드의 이름을 결정하고 메소드를 사용한 템플릿 메소드에 의해 처리를 기술하는 것은 가능함
- 실제의 처리 내용은 하위 클래스에서 결정하지만 추상 클래스의 단계에서 처리의 흐름을 형성하는 것은 중요함

### 상위 클래스와 하위 클래스의 협조
- 상위 클래스와 하위 클래스는 서로 협조하면서 프로그램을 구축함
- 상위 클래스에서 기술을 많이 하면 하위 클래스에서는 기술하기 편하게 되지만, 하위 클래스의 자유는 줄어듬
- 반대로 상위 클래스에서 기술을 적게하면 하위 클래스의 기술이 어렵게 되고, 각각의 하위 클래스에서 처리의 기술이 중복될지도 모름
- Template Method 패턴에서는 처리의 골격을 상위 클래스에서 기술하고 구체적인 내용은 하위 클래스에서 수행함
- 어늘 레벨에서 처리를 분배할 지, 어떤 처리를 상위 클래스에 두고 어떤 처리를 하위 클래스에 둘 것인지를 정한 메뉴얼은 없고 설계대로 하면 됨

### 안드로이드 활용
- AsyncTask 즉 안드로이드에서 비동기 처리를 할 때 Template Method 패턴을 사용해서 쓰레드 처리를 관리하는 부분이 활용되는데 자세하게 기술하지 않는 이유는 비동기 처리를 AsyncTask로 하는 방법은 Coroutine, RxJava등 더 효율적으로 사용하기 때문에 상세하게 기술을 하진 않음
```java
public class MainActivity extends Activity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    // 버튼을 클릭하면 파일 다운로드 경로를 파라미터로 AsyncTask 실행
    public void OnClick(View view) {
        switch (view.getId()) {
            case R.id.button:
                try {
                    new DownloadFilesTask().execute(new URL("파일 다운로드 경로1"));
                } catch (MalformedURLException e) {
                    e.printStackTrace();
                }
                break;
        }
    }

    private class DownloadFilesTask extends AsyncTask {
        @Override
        protected void onPreExecute() {
            super.onPreExecute();
        }

        @Override
        protected Long doInBackground(URL... urls) {
                // 전달된 URL 사용 작업

            return total;
        }

        @Override
        protected void onProgressUpdate(Integer... progress) {
            // 파일 다운로드 퍼센티지 표시 작업
        }

        @Override
        protected void onPostExecute(Long result) {
            // doInBackground 에서 받아온 total 값 사용 장소
        }
    }
}

```

- AsyncTask를 상속받은 클래스가 해당 작업을 구체화 시키고 있음

- 어떻게 보면 위와 같이 안드로이드 프레임워크 사용에 있어서 이런 템플릿 패턴이 어느정도 기저에 깔려있다고 봐도 됨