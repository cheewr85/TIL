## Null Safety
- Null에 대해서 안전함, 코틀린의 특징

- Null vs 0
	- 0 : 휴지를 다 쓰고 휴지심만 남은 상태
	- Null : 휴지심도 없는 상태, 존재하지 않는 상태, 모르는 상태(관리할 수 없는 상태)

- Null이 안전하지 않은 이유
	- 0 + 10 = 10
	- Null + 10 = ? -> 에러
	- button.setOnClickListener
	- null.setOnClickListener -> 에러
	- 항상 체크해줘야함
	- if(number != null) number+=10
	- if(button != null) button.setOnClickListener

- 이러한 Null 체크를 사람의 기량이 아닌 문법적인 요소로 만들어서 Null Safe하게 만듬, 코틀린이 Null Safety하기 위해서 사용하는 문법
	- ? : Null이 아니라면 이하 구문 실행
	- !! : Null이 아님을 개발자가 보장한다(null일 경우 에러가 뜸)
	- 사용방법
	- button?.setOnClickListener -> ?앞의 있는 것이 null이 아니라면 실행한다는 의미
	- button!!.setOnClickListener -> 확실히 null이 아님

### 실습
```Kotlin
package techtown.org.fastcampus

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle

class NullSafety : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_null_safety)


        val number : Int = 10 // null이 될 수 없는 Int 타입을 의미
        val number1 : Int? = null // null이 될 수 있는 Int 타입을 의미

//        val number3 = number1? + number // 이런식으로 표현할 순 없음
        val number3 = number1?.plus(number) // number1이 null 이므로 ?이하를 실행 안 함 그래서 number3는 null로 됨

        // 삼항연산자 -> 엘비스 연산자(?:)
        // Null safety를 위한 도구
        val number4 = number1 ?: 10 // number1이 null이 아니면 number1이 들어가고 null 이면 10이 들어감



    }


    fun plus(a: Int, b: Int?): Int{
        if(b != null) return a + b
        else return a
    }

    fun plus2(a: Int, b: Int?): Int?{ // 확실히 명시를 해줘야 null safety를 활용할 수 있음
        return b?.plus(a)
    }
}
```
```Kotlin
// !! -> 개발자가 null이 아님을 보장함
//        val number5 : Int = number1 + 10 // 에러가 뜸 number1이 null일수도 있고 Int일수도 있으므로 에러가 뜸
        val number5 : Int = number1!! + 10 // 그러므로 확실히 null이 아님은 알 때는 !!를 통해서 개발자가 null이 아님을 보장할 수 있음
```

- lateinit
	- init -> 초기값 셋팅
	- late -> 늦게 나중에
	- 초기값을 나중에 셋팅 해주겠다
	- 초기값이 셋팅 되지 않았을 때 호출하면 에러가 발생한다

### 실습
```Kotlin
package techtown.org.fastcampus

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.util.Log

class NullSafety : AppCompatActivity() {

    lateinit var lateCar : Car

    class Car(var number : Int){
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_null_safety)

        lateCar = Car(10)
        Log.d("Car", "lateCar : " + lateCar)

    }


  
}
```
```Kotlin
package techtown.org.fastcampus

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.util.Log

class NullSafety : AppCompatActivity() {

    lateinit var lateCar : Car

    class Car(var number : Int){
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_null_safety)


		Log.d("Car", "lateCar : " + lateCar)
        lateCar = Car(10)

    }


   
}
```
- 위처럼 순서를 바꿔 Log를 만들어 먼저 찍으면 에러가 뜸
- 만일 그냥 var을 쓰면 초기화하라고 에러가 뜸, 이를 피하기 위해서 lateinit설정함, 나중에 초기화를 하겠다
- 근데 만일 2번째 예시처럼 Log를 먼저 찍으면 초기화가 되지 않았으므로 에러가 발생함
- 1번째 예시처럼 쓰면 정상적으로 나옴 즉, 나중에 쓰기 위해서는 사용 전 반드시 초기화를 해야함
- 확인하기 힘드므로 사용시 반드시 초기화 확인 필요