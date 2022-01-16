## Adapter 패턴
- adapter는 adapt(개조) 시키는것, AC 어댑터의 역할은 직류 12볼트의 컴퓨터를 교류 100볼트의 환경에 맞게 바꾸는 것임
- 이를 프로그래밍으로 생각을 한다면 이미 제공되어 있는 것을 그대로 사용할 수 없을 때, 필요한 형태로 교환하고 사용하는 일이 많은데 이미 제공되어 있는 것과 필요한 것 사이의 차이를 없애주는 디자인 패턴이 Adapter 패턴임
- Adapter 패턴을 Wrapper 패턴이라고도 함 무엇인가를 한 번 포장해서 다른 용도로 사용할 수 있게 교환해주는 것이 wrapper이며 adapter임
- 두 가지 종류가 존재함
    - 클래스에 의한 Adapter 패턴(상속을 사용한 Adapter 패턴)
    - 인스턴스에 의한 Adapter 패턴(위임을 사용한 Adapter 패턴)

### 예제1(상속을 사용한 Adapter 패턴)
![one](/img/DesignPattern/Adapter/one.png)

- 제공되고 있는 것 : Banner 클래스(showWithParen, showWithAster)
- 교환장치(Adapter) : PrintBanner 클래스
- 필요한 것 : Print 인터페이스(printWeak, printStrong)
```java
public class Banner {
        private String string;
        public Banner(String string) {
                this.string = string;
        }
        public void showWithParen() {
                System.out.println("(" + string + ")");
        }
        public void showWithAster() {
                System.out.println("*" + string + "*");
        }
}
```
```java
public interface Print {
        public abstract void printWeak();
        public abstract void printStrong();
}
```
```java
public class PrintBanner extends Banner implements Print {
        public PrintBanner(String string) {
                super(string);
        }
        public void printWeak() {
                showWithParen();
        }
        public void printStrong() {
                showWithAster();
        }
}
```
- Banner 클래스를 사용해서 Print 인터페이스를 충족시키는 클래스를 만드는 일을 함
- PrintBanner 클래스가 어댑터 역할을 함 제공되어 있는 Banner 클래스를 상속해서 필요로 하는 Print 인터페이스를 구현함

```java
public class Main {
        public static void main(String[] args) {
                Print p = new PrintBanner("Hello");
                p.printWeak();
                p.printStrong();
        }
}
```
- Main 클래스 내에서는 PrintBanner 인스턴스를 Print 인터페이스형의 변수로 대입함
- Main 클래스는 Print라는 인터페이스를 사용해서 프로그래밍 함
- Main 클래스를 전혀 바꾸지 않고 PrintBanner 클래스의 구현을 바꿀 수 있음(Banner 클래스나 showWithParen 메소드나 showWithAster 메소드는 Main 클래스의 소스 코드 상에서는 완전히 감추어짐)

### 예제2(위임을 사용한 Adapter 패턴)
![one](/img/DesignPattern/Adapter/two.png)

- 위임을 사용한다는 것은 어떤 메소드의 실제 처리를 다른 인스턴스의 메소드에 맡기는 것을 의미함

```java
public class Banner {
        private String string;
        public Banner(String string) {
                this.string = string;
        }
        public void showWithParen() {
                System.out.println("(" + string + ")");
        }
        public void showWithAster() {
                System.out.println("*" + string + "*");
        }
}
```
```java
public abstract class Print {
        public abstract void printWeak();
        public abstract void printStrong();
}
```
```java
public class PrintBanner extends Print {
        private Banner banner;
        public PrintBanner(String string) {
                this.banner = new Banner(string);
        }
        public void printWeak() {
                banner.showWithParen();
        }
        public void printStrong() {
                banner.showWithAster();
        }
}
```
```java
public class Main {
        public static void main(String[] args) {
                Print p = new PrintBanner("Hello");
                p.printWeak();
                p.printStrong();
        }
}
```
- Print는 인터페이스가 아니고 추상클래스로 가정함
- Banner 클래스를 사용해서 Print 클래스와 동일한 메소드를 갖는 클래스를 실현함
- 2개의 클래스를 동시에 상속을 할 수 없기 때문에 PrintBanner 클래스는 banner 필드에서 Banner 클래스의 인스턴스를 가짐, 이 인스턴스는 PrintBanner 클래스의 생성자에서 생성함
- printWeak 및 printStrong 메소드에서는 banner 필드를 매개로 showWithParen, showWithAster 메소드를 호출함, 이번에는 필드를 경유해서 호출함, 위임을 하는 것
- PrintBanner 클래스에서 처리하는 게 아닌 Banner의 인스턴스인 showWithParen 메소드에 위임함

### 패턴의 등장인물
- Target(대상)의 역할
    - 지금 필요한 메소드를 결정함, 예제에서 Print 인터페이스(상속의 경우)나 Print 클래스(위임의 경우)가 이 역할을 함
- Client(의뢰자)의 역할
    - Target 역할의 메소드를 사용해서 일을 함 ⇒ Main 클래스
- Adaptee(개조되는 쪽)의 역할
    - 이미 준비되어 있는 메소드를 가지고 있는 역할을 함
    - Banner 클래스가 이 역할을 함, Adaptee역의 메소드가 Target 역할의 메소드와 일치하면 Adapter의 역할은 필요 없음
- Adapter의 역할
    - Adaptee 역할의 메소드를 사용해서 어떻게든 Target 역할을 만족시키기 위한 것
    - 예제 프로그램에서는 PrintBanner 클래스가 Adapter 역할을 함
    - 클래스에 의한 Adapter 패턴의 경우 Adapter의 역할은 상속을 사용한 Adaptee의 역할을 이용하지마 인스턴스에 의한 Adapter 패턴의 경우에는 위임을 사용한 Adaptee의 역할을 이용함

### 사고력 키우기
- 이미 존재하고 있는 클래스를 이용하는 경우도 있음, 그 클래스가 충분한 테스트를 받아서 버그가 적으며 실제로 지금까지 사용된 실적이 있다면 어떻게든 그 클래스를 부품으로 재이용하고 싶을 것
- Adapter 패턴은 기존의 클래스를 개조해서 필요한 클래스를 만듬, 이 패턴으로 필요한 메소드를 발빠르게 만들 수 있음
- 버그가 발생해도 기존의 클래스에는 버그가 없으므로 Adapter 역할의 클래스를 중점적으로 조사하면 됨

![one](/img/DesignPattern/Adapter/three.png)
![one](/img/DesignPattern/Adapter/four.png)

- 비록 소스가 없더라도
    - Adpater 패턴은 기존의 클래스를 전혀 수정하지 않고 목적한 인터페이스(API)에 맞추려는 것
    - 기존 클래스의 사양만 알면 새로운 클래스를 만들 수 있음
- 버전 업과 호환성
    - 구 버전과 신 버전을 공존시키고 유지와 보수도 편하게 하기 위해서 Adapter 패턴이 도움이 되는 경우가 있음
    - 신 버전을 Adaptee 역할로 하고, 구 버전을 Target 역할로 하며 신 버전의 클래스를 이용해서 구 버전의 메소드를 구현하는 Adapter 역할의 클래스를 만듬
- 동떨어진 클래스
    - Adapter 역할과 Target 역할의 기능이 지나치게 동떨어진 경우에는 Adapter 패턴을 사용할 수 없음

### 추상 클래스 & 인터페이스 차이
- 위의 예제에서 보면 추상 클래스 사용 시에는 부모 클래스를 상속하여 부모 클래스가 가진 기능들을 구현하는 경우 사용을 함 즉, Print 클래스를 상속받고 해당 메소드를 구현하는데 있어서 Banner라는 인스턴스를 활용해서 쓴 것임
- 인터페이스의 경우 다른 조상 클래스를 상속해도 같은 기능이 필요한 경우 사용함, 클래스와 별도로 구현 객체가 같은 동작을 한다는 것을 보장하는 것인데 PrintBanner 클래스에서 Banner 클래스를 상속받아서 구현을 하여 String을 생성하였지만 Print 인터페이스를 구현하고 해당 메소드를 구현할 때 Banner 클래스를 상속받았으므로 그 클래스의 메소드를 사용해서 구현하였음
- 결과적으로 추상 메소드 구현을 강제하는 것은 동일하나 위에서 설명한대로 상속과 위임이라는 방식의 차이가 존재함

### 안드로이드 예제
- RecyclerView라는 곳에서 Adapter 패턴을 사용함, 이때 이 Adapter는 위임을 사용한 패턴임
- 즉 RecyclerView라는 곳에 받은 데이터에 대해서 리스트 형태로 쭉 보여줘야 하는데 그 보여주는 것을 이 Adapter 패턴을 통해서 처리하는 것임, 그렇게 하면 데이터를 네트워크를 통해서 받던 내부 DB로 받던 아니면 직접 만들어서 보내던 Adapter에 설정에 상관없이 그대로 받아서 넘길 수 있음
```java
public class SimpleTextAdapter extends RecyclerView.Adapter<SimpleTextAdapter.ViewHolder> {

    private ArrayList<String> mData = null ;

    // 아이템 뷰를 저장하는 뷰홀더 클래스.
    public class ViewHolder extends RecyclerView.ViewHolder {
        TextView textView1 ;

        ViewHolder(View itemView) {
            super(itemView) ;

            // 뷰 객체에 대한 참조. (hold strong reference)
            textView1 = itemView.findViewById(R.id.text1) ;
        }
    }

    // 생성자에서 데이터 리스트 객체를 전달받음.
    SimpleTextAdapter(ArrayList<String> list) {
        mData = list ;
    }

    // onCreateViewHolder() - 아이템 뷰를 위한 뷰홀더 객체 생성하여 리턴.
    @Override
    public SimpleTextAdapter.ViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
        Context context = parent.getContext() ;
        LayoutInflater inflater = (LayoutInflater) context.getSystemService(Context.LAYOUT_INFLATER_SERVICE) ;

        View view = inflater.inflate(R.layout.recyclerview_item, parent, false) ;
        SimpleTextAdapter.ViewHolder vh = new SimpleTextAdapter.ViewHolder(view) ;

        return vh ;
    }

    // onBindViewHolder() - position에 해당하는 데이터를 뷰홀더의 아이템뷰에 표시.
    @Override
    public void onBindViewHolder(SimpleTextAdapter.ViewHolder holder, int position) {
        String text = mData.get(position) ;
        holder.textView1.setText(text) ;
    }

    // getItemCount() - 전체 데이터 갯수 리턴.
    @Override
    public int getItemCount() {
        return mData.size() ;
    }
}
```
- 위의 예시를 본다면 데이터 리스트 객체를 전달받는 것이 있는데 이는 위의 위임예제에서 PrintBanner에서 Banner를 인스턴스로 생성한 것과 유사함
- 즉, mData는 매개변수로 넘겨받고 해당 데이터에 대해서 전체 데이터 개수 리턴과 뷰홀더에 아이템 표시 등의 역할을 할 수 있는 것임
- 그럼 그런 Banner 클래스는 아래와 같이 해당 View가 속해있는 실제 클래스 파일에서 데이터를 Adapter에 넘겨주는 것임

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        // ... 코드 계속

        // 리사이클러뷰에 표시할 데이터 리스트 생성.
        ArrayList<String> list = new ArrayList<>();
        for (int i=0; i<100; i++) {
            list.add(String.format("TEXT %d", i)) ;
        }

        // 리사이클러뷰에 LinearLayoutManager 객체 지정.
        RecyclerView recyclerView = findViewById(R.id.recycler1) ;
        recyclerView.setLayoutManager(new LinearLayoutManager(this)) ;

        // 리사이클러뷰에 SimpleTextAdapter 객체 지정.
        SimpleTextAdapter adapter = new SimpleTextAdapter(list) ;
        recyclerView.setAdapter(adapter) ;
    }
```
- 여기서는 러프하게 데이터를 넘겨주었는데, 이제 이 데이터를 네트워크 통신의 결과값 혹은 DB에 접근했을 때의 결과값등 다양하게 넘겨줄 수 있고 또 Adapter 내부에서 ArrayList가 아닌 다른 형태로 받아서 처리할 수도 있고 그에 맞춰서 다른 형태로 넘겨주면 됨, 이런식으로 Adapter 패턴을 활용가능함

![one](/img/DesignPattern/Adapter/five.png)

- 위와 같이 화면을 그릴 수 있게됨 Adapter 패턴을 활용해서 RecyclerView를 활용하면 부가적으로 이 View를 그리기 위해서 별도로 ViewHolder를 선언하여 만드는 것과 해당 객체를 생성해서 리턴하는 것은 생략하겠음
