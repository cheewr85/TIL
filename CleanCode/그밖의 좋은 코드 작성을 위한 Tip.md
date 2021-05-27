### 예외
- 예외
    - 예외(Exception)는 예외 상황에 사용되도록 의도된 도구인 만큼 예외를 잘 사용하는 것이 좋은 코드를 작성하는 데에 중요함
- 에러 코드
    - 에러 코드는 코드 가독성을 심하게 해침, 에러 코드가 비즈니스 로직과 예외 처리 로직을 한 곳에 혼재시켜버리기 때문임
    - 함수를 호출한 코드는 매번 조건절을 통해 에러 코드를 검사해야 하기 때문에 중괄호 중첩 문제를 자주 일으킴
    - 에러 코드를 검사하고 처리하는 로직이 코드 전방위에 흩어질 것임
    - 결국 에러 코드 관련 로직으로 도배가 될 것임
    - 에러 코드를 검사하지 않고 넘어가면 에러가 발견되지 않게 됨
    - 에러 상황에 예외를 던지면 전방위에 걸쳐 흩어져 있던 에러 코드 검사 로직이 전부 사라져 코드의 가독성이 향상될 것임
    - 실수로 에러 처리를 하지 못해도 예외가 밖으로 전파되기 때문에 실수를 바로 잡기가 더 쉬움
    - 예시
    ```java
    Elevator elevator = ElevatorManager.getOptimalElevator(movingRequest);

    if(elevator.getStatus() == Elevator.VALID_STATUS){
        ElevatorAction elevatorAction = 
            elevator.moveTo(movingRequest.getDepartureFloor());
        
        if(elevatorAction.getStatus() == ElevatorAction.ARRIVED){
                ElevatorAction elevatorAction = 
                    elevator.moveTo(moveRequest.getDestinationFloor());

                if(elevatorAction.getStatus() == ElevatorAction.ARRIVED){
                    ...
                }else{
                    logger.error("Elevator does not move.");
                    status = elevatorAction.getStatus();
                }
        }else{
                logger.error("Elevator does not move.");
                status = elevatorAction.getStatus();
        }
    }else{
        ...
    }
    ```

- 위의 예시를 예외를 던지도록 리팩토링 하면 아래와 같이 쓸 수 있음
```java
Elevator elevator = ElevatorManager.getOptimalElevator(movingRequest);
elevator.moveTo(movingRequest.getDepartureFloor());
elevator.moveTo(movingRequest.getDestinationFloor());
```

- 예외(Exception) 관련 TIP
    - 예외를 잡았다면 예외 상황을 복구하거나 적절히 처리해야함
        - 예외는 감추어져서는 안됨, 예외를 잡고 아무것도 하지 않거나 간단히 로그만 찍고 넘어간다면 심각한 문제상황이 생김
        - 예외처리가 어렵다고 판단되면 더 적절한 곳에서 예외를 처리할 수 있도록 예외를 밖으로 전파하는 것이 나음
    - 최대한 표준 예외를 사용하는 것이 좋지만 예외 전환을 고려해 보는것도 좋음
        - 새로 던질 예외가 비즈니스 로직에 더 적합한 의미가 있거나 특정 사용 기술에 대한 종속을 피하기 위함이거나 함수의 추상화 수준에는 처리되어야 할 예외가 적합하지 않은 경우여야만 함
        - 예외 전환시 원인이 되는 예외를 담아 함께 던져주어야 원인 파악에 도움이 됨
    - 예외는 예외 상황에만 사용함
        - 비즈니스 로직의 일환으로 예외를 사용하는 anti pattern을 보게 되면 혼란을 느낄 수 있음
        - 예외가 일종의 정상적인 흐름의 일부지만 생성에 큰 비용이 드는 객체임
        - 자주 발생하는 만큼 성능적으로도 좋지 않음
    - 예외는 예외 상황 파악에 필요한 실패 관련 메세지를 담아야함
    - 예외 발생 이전과 예외 발생 이후에 어플리케이션의 상태에 어떤 변화가 있어서는 안됨
    - 예외 클래스는 보통 `Exception` 으로 끝나도록 이름 지음
    - 예외 처리보다 예외 상황을 사전에 검사하거나 null을 반환하지 않기 같이 애초에 예외가 발생하지 않게 코드를 작성하는 것을 우선해야함

### 그밖의 좋은 코드 작성을 위한 Tip1
- 변수의 수직 유효 범위
    - 변수의 수직 유효 범위란 변수가 처음 생성되고 닫는 중괄호를 만나 소멸할 때까지의 코드상의 수직 범위(거리)를 의미함
    - 변수의 수직 유효 범위는 좁을수록 좋음, 변수는 실제로 사용될 때 선언해 유효 범위가 넓어지지 않도록 함

- try 블록의 범위
    - try절도 좁을수록 좋음, 가급적 예외가 발생할 가능성이 있는 지점만을 감싸주는 것이 좋음, 너무 넓은 범위를 감싸면 가독성 저하 발생뿐만 아니라 올바른 예외 처리 기회를 놓칠 수 있음

- if절 안의 코드는 딱 한 줄만
    - if절 안의 코드는 딱 한 줄만 넣으려고 시도하는 것이 좋음
    - 중괄호 안에 복잡한 코드를 욱여 넣지 말고 그 코드를 밖으로 빼내어 다른 함수로 정의하고 이를 호출하는 게 중괄호 중첩을 피하기 좋은 방법임
    - try절로 감싸진 코드가 있다면 이 코드를 밖으로 빼내어 함수로 만들고 중괄호 중첩이 발생하기 좋은 try절 내부에서 이 함수를 호출하도록 코드를 작성하는게 좋음

- 클래스가 많아질 경우
    - 함수를 분리하고 분리된 함수들을 더 적합한 작은 클래스들로 분리하는 과정이 필요함
    - 팀내 룰을 따르는게 좋지만 클래스의 역할이 잘 정해지고 이름을 충분히 잘 짓는다면 어느정도 완화 가능한 문제임

### 그밖의 좋은 코드 작성을 위한 Tip2
- 무분별한 임시 변수 사용
    - 아래와 같이 임시변수를 사용하는 경우
    ```java
    String temp = func();
    return temp;
    ```
    - 그냥 `return temp();` 하는게 좋음, 임시변수를 무분별하게 사용할수록 가독성에 큰 어려움이 생김
    - 도메인 로직이 복잡할수록, 함수의 길이가 길수록, 특히 변수의 수직 유효 범위가 클수록 이런 의미 없는 변수는 혼란을 일으킴
    - 임시 변수는 임시 변수가 가독성을 향상시켜줄 수 있는 경우에만 사용해야함, 계산식이나 함수 호출 구문의 길이가 길 때는 임시 변수를 사용하는게 더 나을 수 있음(단 temp 같은 이름은 피해야함)
    
- 쿼리와 명령 분리
    - 함수는 상태의 변화를 일으키지 않고 결과값을 반환하는 **쿼리**와 시스템 상태를 변경시키는 **명령** 둘 중 하나여야만 함
    - 자바에서는 Map(swift, python에서 Dictionary) 클래스에는 put()이라는 메서드가 있음, 이 메서드는 Map 자료구조에 key와 value를 저장함, void일 것을 예상되지만 그렇지 않은 반환 타입임, put을 할 때는 key에 해당하는 기존 value를 반환함
    - 쿼리는 상태 변경 없이 결과값을 반환하기 때문에 사용자가 이 함수를 걱정 없이 호출함, 다른 부작용이 없으므로 HTTP GET 메서드
    - 하지만 한 함수가 쿼리의 역할과 명령의 역할 모두를 수행하면 어떤 부작용을 일으킬지 그리고 애매한 동작으로 인해 버그의 원인이 되기도 함
    - 그렇기 때문에 가능하면 쿼리와 명령을 분리하는 습관을 들이는게 좋음

- 수정말고 반환하라
    - 아래 코드와 같이 공유 변수 `totalUsedPoints` 의 값을 수정하는 함수를 호출하는 것보다
    ```java
    int totalUsedPoints = 0;
    calculateTotalUsedPoint();

    void calculateTotalUsedPoint(){
        for(Integer usedPoint : pointUsedHistories)
        totalUsedPoints += usedPoint;
    }
    ```
    - 아래와 같이 수정될 값을 반환하는 함수를 사용하도록 해야 공유 변수의 상태를 더 명확히 추적할 수 있음
    - 수정되는 데이터는 수정 추적이 용이해야만 함
    - 이는 무슨 일을 하는지를 좀 더 쉽게 알 수 있게 해준다는 장점도 있음
    ```java
    int totalUsedPoints = calculateTotalUsedPoint();

    int calculateTotalUsedPoint(){
        int totalUsedPoints = 0;

        for(UsedPoint point : usedPoints)
            totalUsedPoints += point.amount();

        return totalUsedPoints;
    }
    ```

- Tell, Don't ask
    - 아래 예시와 같은 코드가 있다고 가정, ElevatorManager와 Elevator 클래스가 있다고 가정

    ```java
    function moveElevator(int floorNumber) {
        if(elevator.currentFloor == floorNumber)
            return;

        elevator.move(floorNumber);
        elevator.currentFloor = floorNumber;
    }
    ```
    - ElevatorManager 클래스는 Elevator의 세세한 부분을 잘 알고 있음, 이런 코드와 같이 다른 객체의 내부 상태에 접근하는(직접 가져와서 특정 값과 비교)방식은 변경에 취약함
    - 만일 건물의 층을 의미하는 Floor라는 타입이 추가되었다고 한다면 Elevator 클래스의 currentFloor 타입이 변경될 것이고 그러면 위에서 사용하는 moveElevator 함수도 변경되어야 함
    - 아래와 같이 변경하면 좋음
    ```java
    class Elevator{
         private integer currentFloor;

        function move(int floorNumber){
            if(currentFloor == floorNumber)
               return;

            moveInternal()

            this.currentFloor = floorNumber
        }
    }

    class ElevatorManager{
        private Elevator elevator;

        function moveElevator(int floorNumber){
            elevator.move(floorNumber);
        }
    }
    ```
    - 위의 코드에서는 ElevatorManager가 Elevator의 내부 데이터의 변경에 영향을 받지 않음
    - 이처럼 객체에 내부 상태를 ask(`elevator.currentFloor == floorNumber`)하지 말고 tell(`move()`)하면 캡슐화를 깨지 않고 변경에 닫힌 코드 작성을 가능하게 함, ask 방식에서 자주 발생하는 코드 중복을 피할 수 있음

### 그밖의 좋은 코드 작성을 위한 Tip3
- null 반환
    - null을 반환하는 함수는 만들지 않는게 좋음
    - null을 반환할 수 있는 함수를 호출하는 코드는 꼭 null 검사를 하는게 좋음
    - 값이 없음을 표현하는 값을 반환하려고 할 때는 널 오브젝트 반환을 고려하면 됨
    - 널 오브젝트란 값이 없는 상태를 대신하여 아무 일도 하지 않는 객체(또는 값이 없는 경우에 필요한 기본 동작을 하는 객체)를 의미함
    - 아래와 같은 코드를 작성
    ```java
    class NoPet extends Pet {
        @Override
        public void howl(){
            return;
        }
    }
    ```
    - 널 오브젝트를 반환하면 호출자 코드에서 실수로 null 검사를 하지 않아 null 관련 예외나 예기치 못한 버그가 발생하는 경우를 방지할 수 있음
    - 널 오브젝트 패턴으로 함수 호출자 코드가 지저분해진다면 쓰느니만 못함

- 배열이나 컬렉션은?
    - 값이 없을 때는 빈 배열이나 빈 컬렉션을 반환하는 것을 고려해보는게 좋음
    - 여기서 아래처럼 빈 리스트를 매번 생성하는 것보다
    ```java
    return new ArrayList<>();
    ```
    - 아래와 같이 이미 존재하는 객체를 사용하는게 좋음
    ```java
    return Collections.emptyList()
    ```
    - 널 오브젝토 또한 마찬가지로 매번 만들 필요 없이, 여러 곳에서 사용해도 문제가 없으면 싱글톤 오브젝트로 만들어두고 재사용하는게 좋음

- Optional
    - 코틀린에서는 null safety 관련 지원을 함, 자바에서는 null을 반환하는 것이 아니라 Optional을 대안으로 쓸 수 있음
    - Optional을 쓰는 이유는 호출자 코드에 null이 반환될 수 있음을 알리고 이를 처리하는 코드를 강제하여 실수로 null 검사를 하지 않는 경우를 방지하기 위해서 함
    - Optional로부터 실제 사용할 결과값을 가져오려면 null일 경우 default 객체를 반환하도록 할 지 다른 예외를 던질지 아니면 그냥 NullPointException이 발생하도록 둘지를 호출자가 정해야함, 상황에 다라 if 조건문으로 null 검사를 하는 것보다 코드 가독성을 향상시킬 수 있음
    - Optional을 반환하는 메서드는 절대 null을 반환해서는 안됨, 자바를 사용하는 누구도 Optional을 반환하는 함수가 null을 반환할 거라고 생각하지 않기 때문임, 지키지 않는다면 호출자 코드에는 NullPointException이 발생할 것임

- if-else
    - if-else 구문은 아래 코드와 같이 비즈니스 로직 이곳저곳에 중복되는 경향이 있음
    ```java
    public interface PocketMon {
        void attack();
        void move();
    }

    public class Pikachu implements PocketMon{

        @Override
        public void attack(){
            print("Mega volt!");
        }

        @Override
        public void move(){
            print("Fast moving");
        }
    }

    public class TurtleKing implements PocketMon {

        @Override
        public void attack(){
            print("Water cannon!");
        }

        @Override
        public void move(){
            print("Swimming");
        }
    }

    public class PocketMonFactory{
        public static PocketMon createPocketMon(String pocketMonName){
            if("Pikachu".equals(pocketMonName)){
                return new Pikachu();
            }else if("Pigeon".equals(pocketMonName)){
                return new Pigeon();
            }else if("TurtleKing".equals(pocketMonName)){
                return new TurtleKing();
            }
            ...
            else{
                throw new UnknownPocketMonException("Unkown pocketmon :" + pocketMonName);
            }
        }
    }

    public static void main(String[] args){
      PocketMon pocketMon = PocketMonFactory.createPocketMon(args[1]);
      pocketMon.move();
      pocketMon.attack();
    }

    ```
    - 위처럼 if-else가 PocketMonFactory 클래스 외부로 퍼져나가지 않게

- else를 없애라
    - 위와 같은 코드 상황에서 else를 없앨 방법을 생각함, 가급적 if절에서 조건을 검사한 후 바로 리턴하거나 예외를 던지도록 코드를 수정해 else 절을 없애 주는게 중괄호 중첩을 막는 좋은 방법임
    ```java
    for(Apple apple : apples){
      if(apple.isSellableQuality()){
        //blar blar
        //blar blar
        //blar blar
        fruitBox.add();
      }else{
        throw new BadQualityAppleFoundedException();
      }
    }
    ```
    - 위 코드를 아래와 같이 수정해 보는 것
    ```java
    for(Apple apple : apples){
      if(apple.isNotSellableQuality())
        throw new BadQualityAppleFoundedException();

      //blar blar
      //blar blar
      //blar blar
      fruitBox.add();
    }
    ```
    - 만약 else를 없애기 어려운 상황이라면 if 절에는 정상적인 상황에 대한 조건을 두고 비정상적인 상황을 else절에 두는 게 직관상 좋음

### 그밖의 좋은 코드 작성을 위한 Tip4
- 지식의 저주
    - `if(category == "S001")` 같은 코드는 과연 맞을까?
    - 아마 문자열 타입 상수형 변수 이름(`ProductCategory.SNEAKERS`)을 사용해야할 자리에 도메인에 익숙한 나머지 문자열 리터럴을 써버린 케이스임
    - 문자열 상수, 인트 타입 상수로 하여금 하드코딩이 된 것
    - 이처럼 저런식의 하드코딩을 하는 것이 아니라 처음 보는 사람도 이해할 수 있도록 잘 지은 상수를 사용하거나 `isSneakers(variable)` 과 같은 함수를 사용해서 조건문을 캡슐화하는 것이 좋음
    - 더 좋은 방법은 문자열, 인티저 타입 상수 말고 다른 방법이 있는지 알아보는 것 자바라면 enum을 사용하는게 좋음

- boolean, enum
    - 불리언이 사용되야 할 곳에 다른 타입을 사용하지 마라 즉, 참일때 문자열 yes, 거짓일 때 문자열 no이런 짓을 하지마라
    - 아래와 같이 설정한 코드가 있음
    ```java
    public class YutNoriConstant {
        public static final int DO = 1;
        public static final int GAE = 2;
        ...
        public static final int MO = 0;
    }

    if(sticks.flippedCount() == YutNolEConstant.MO)
    // if(sticks.flippedCount() == 0)와 동일
    ```
    - 하지만 위와 같이 쓰면 직접 숫자를 써버리는 실수가 발생할 확률이 큼 이때 아래와 같이 enum을 사용함
    ```java
    public enum Yut{
        DO(1), Gae(2) ... ,Mo(0);

        private static Map<Integer, Yut> possibleCards = new HashMap<>();

        private int flippedCount;

        static{
            for(Yut yut : values())
                possibleCards.put(yut.flippedCount, yut);
        }

        Yut(int flippedCount){
            this.flippedCount = flippedCount;
        }

        public static Optional<Yut> fromFlippedCount(int flippedCount){
            return Optional.ofNullable(possibleCards.get(flippedCount));
        }
    }
    ```
    - Yut 타입 멤버 변수를 두어서 Yut.fromFlippedCount() 메서드를 사용하면 쉽게 Yut 객체를 가져올 수 있음
    - enum으로 바뀌었기 때문에 컴파일러가 알 수 있음

### 그밖의 좋은 코드 자성을 위한 Tip5
- 문맥
    - 객체가 갖는 값(상태)과 이를 처리하는 로직(행위)은 한 곳에서 관리 되어야 좋음
    - 객체의 상태와 먼 거리에 있는 코드에서 행위가 이루어지면 유지보수와 협업에 좋지 않음

- 일급 컬렉션
    - 컬렉션을 포함한 클래스에는 반드시 컬렉션 외의 다른 멤버 변수가 없어야 한다고 함
    - 컬렉션이 기본으로 제공하는 add, remove, iterate와 같은 기본 동작 외에 validation, filtering 등 추가 로직이 필요한 경우 일급 컬렉션을 고려해볼 것을 추천함
    - 아래와 같이 필터링을 통해 사과를 고르는 작업을 아주 간략하게 표현함, 아래와 같이 필터링 등 로직이 필요할 경우, 아래처럼 직접 사용하는 것은 지양함
    ```java
    Set<Apple> applesToBeSold = new HashSet<>();

    for(Apple apple : apples)
        if(apple.isSellableQuality())
            applesToBeSold.add(apple);
    ```
    - 아래와 같이 Apple의 Set만 멤버 변수로 정의한 클래스를 만들고 filtering 작업을 이 클래스 내부에 담는 것이 좋음, 아래와 같이 필터링 작업이 ApplesToBeSol라는 클래스 한 곳에 모두 담겨있음
    ```java
    class ApplesToBeSold {
        private Set<Apple> apples = new HashSet<>();
        
        public void add(Apple apple){
            if(apple.isSellableQuality())
                apples.add(apple);
        }
    }

    ApplesToBeSold applesToBeSold = new ApplesToBeSold();

    for(Apple apple : apples)
        applesToBeSold.add(apple);
    ```

- enum
    - 아래와 같이 요일별 감정 상태를 출력하는 예제를 보면
    ```java
    if(today == DayOfWeek.MonDay){
        System.out.print("Pain.. :( ");
    }
    ...
    }else if(today == DayOfWeek.SaturDay){
        System.out.print("Pleasure!! :D ");
    }else if{today == DayOfWeek.Sunday){
        System.out.print("Fear OTL ");
    }else{
        ?
    }
    ```
    - 이를 DayOfWeek와 기분을 출력하는 행위가 분리되어 있음을 알 수 있음, 이를 enum을 사용하여
    ```java
    public enum DayOfWeek{
        Monday(() -> System.out.print("Pain.. :(")),
        ...
        SaturDay(() -> System.out.print("Pleasure! :)")),
        SunDay(() -> System.out.print("Fear OTL"));

        private Runnable emotionPrinter;

        DayOfWeek(Runnable emotionPrinter){
            this.emotionPrinter = emotionPrinter;
        }

        public void printEmotion(){
            emotionPrinter.run();
        }
    }
    ```
    - 위와 같이 상태와 행위를 DayOfWeek 한 곳에 담을 수 있음, 아래와 같이 한 줄의 메서드 호출로 감정을 출력할 수 있음
    ```java
    today.printEmotion();
    ```

- Primitive 타입 지양
    - 어떤 값을 표현할 때 아래와 같이 원시 타입이나 문자열을 사용하려고 함
    ```java
    String phoneNumber = “+821012345678"
    ```
    - 여기서 국번 정보를 가져오기 위해서 아래와 같이 문자열 파싱이 필요함
    ```java
    phoneNumber.substring(0, 3);
    ```
    - 이를 해결하기 위해서 핸드폰 번호를 나타내는 클래스를 만드는것이 좋음
    ```java
    Class PhoneNumber{
        private CountryCode countryCode;
        private WirelessCarrier wirelessCarrier;
      
        ...
          
        public PhoneNumber(String phoneNumber){
            validatePhoneNumber(phoneNumber);
            ...
        }
      
        private validatePhoneNumber(String phoneNumber){
            // validate phone number format
        }
      
        public CountryCode getCountryCode(){
            return countryCode;
        }
      
        ...
    }
    ```
    - 위와 같이 하면 문자열을 파싱할 필요 없이 getter 호출만으로 국번을 가져올 수 있음 ,그리고 핸드폰 번호라는 상태와 핸드폰 번호 형식의 검증이라는 행위가 한 곳에 담김
    - 정리하자면 원시적인 형태로 정의를 하지 않고 위와 같이 정돈된 형태로 정의하여 사용하는걸 추천함

- 배열(리스트)의 표현력
    - 명시적인 표현인 필요한 곳에 배열이나 리스트를 사용하지 마라
    - 예를 들어 getAllCookies() 함수가 반환하는 배열의 첫 번째 원소는 사용자의 계정, 두 번째 원소는 사용자의 나이, 세 번째 원소는 사용자의 권한을 의미함
    - 여기서 작성해 둔 문서를 보지 않는 한, 아니면 주석을 보지 않는 한 반환값을 알 수가 없음 [0]이라는 인덱스와 userEmail의 연결고리가 없으므로
    - 주석이나 문서로 코드로 충분히 표현할 수 있는 것을 위임하는 것은 좋은 습관이 아님
    - 아래와 같은 코드가 있다고 가정
    ```java
    //cookies[0]는 유저의 이메일을 cookies[1]은 유저의 나이를 cookies[2]는 
    // 유저의 role을 의미한다.
    String[] cookies = getAllCookies();
    String userEmail = cookies[0];
    String userAge = cookies[1];
    String userRole = cookies[2];
    ```
    - 만일 이를 파악하기 위해서는 해당 원소가 무엇을 의미하는지 내부를 샅샅이 뒤져야 할 것임
    - 주석은 코드의 최신 상태에 맞춰 현행화되지 못할 가능성이 큼
    - 주석 의존을 주의하면 된다는 식으로 얼버무려 사용하는 것이 매우 위험함, 가급적 주석 사용을 피하고 표현력 있고 명시적인 코드를 작성하려고 노력해야함
    - 그러므로 이를 의미를 바로 알 수 있도록 추상화된 타입을 반환하도록 바꾸면
    ```java
    User user = getUserInfoFromCookie();
    user.getUserEmail();
    user.getUserAge();
    ...
    ```
    - 위에서 단순하게 배열 인덱스로 표현한 것을 좀 더 명시적으로 표현력이 높아짐, 차라리 맵을 반환해서라도 표현력을 높이는게 좋음

- 하나의 개념, 하나의 상태
    - 하나의 개념엔 하나의 상태만 들어가야 혼란이 없음, 서로 다른 성격의 원소를 타입이 같다는 이유로 동일한 컬렉션에 우겨 넣거나 두 가지 이상의 상태를 한 변수에 담는 경우 혼란이 옴
    - 아래와 같이 쓴다면 혼란을 야기함
    ```java
    String startDate = startAndEndDate.split(";")[0];
    String endDate = startAndEndDate.split(";")[1];
    ```

### 그밖의 좋은 코드 작성을 위한 Tip6
- Don't reinvent the wheel
    - 이미 개발된 기능을 다시 만드는 데 시간을 쓰지 말라, 본인이 사용 중인 클래스에 이미 있는 기능을 직접 개발하거나 다른 라이브러리를 추가해가며 사용하는 개발을 하기도 함
    - 사용하는 언어나 라이브러리 또는 프레임워크에서 제공하는 유틸리티 성 함수를 잘 확인하면 좋음

- 로우레벨 클래스
    - 로우 레벨 클래스의 기능이 필요할 때가 있음, 필요할 때 필요한 클래스를 사용하는 것은 당연함, 단 Don't reinvent the wheel 법칙을 잊으면 안됨

- 기술의 의도
    - 프레임워크를 사용하다 보면 어떤 목적을 달성을 위해 사용 가능한 기능이 여러 가지인 경우가 있음, 이때 어떤 기술을 사용하는 것이 더 적합한가를 정할 때는 사용하려는 후보군이 되는 기술의 설계 목적을 고려해보는게 좋음
    - 예시
        - 컨트롤러(MVC 패턴의 C)의 메서드 호출 전/후에 어떤 작업을 하려고 하는 데 인터셉터가 좋은가 AOP가 좋은가?
        - 컨트롤러의 메서드가 호출되기 전/후에 어떤 작업을 한다는 점에서 위의 인터셉트와 AOP 둘 다 질문자의 목적 달성을 위해 사용될 수 있음, 애매한 상황
        - 이에 대한 답변으로 AOP는 컨트롤러 호출만 고려해서 만들어진 기술이 아니지만 인터셉터는 컨트롤러 호출 전/후의 동작을 고려해서 설계도니 스프링 MVC(웹) 컴포넌트임
        - 둘 다 함수 호출 전/후에 원하는 작업을 하게 해준다는 점에서 기능적으로 같으나 인터셉터는 컨트롤러 전/후의 작업을 고려해 설계된 스프링의 웹 관련 컴포넌트라서 AOP보다 더 특화된 기능을 제공함, 그러므로 더 적합함
    - 이처럼 이러한 의도를 명확히 파악하고 분석해서 사용해야함
    
- 관례
    - 프레임워크를 사용하면서 기어코 남들과 다른 방식으로 개발하는 경우를 본 적이 있음, 기술 사용에도 일종의 약속이 있음
    - 보통 프레임워크는 개발자들이 필요로 하는 방식을 의도하여 기능을 제공할 것이고 실제로 많은 개발자가 이렇게 의도된 방식으로 기능을 사용하기 마련임, 굳이 색다른 방식을 찾으려고 하지 마라 괜히 혼란만 야기함