## Listener
- 익명함수/클래스
- 이름이 없는 함수/클래스
- 이름을 만들어줄 필요가 없음 
- 한 번만 사용함(나중에 부를 일이 없음, 그래서 굳이 이름을 붙여주지 않는 것)
- xml의 적어놓은 뷰를 원하는 동작을 할 수 있게끔 코드로 작성 -> 해당 뷰를 가져온 뒤 이벤트 사용자 input이 발생시 원하는 동작을 진행함, 그때 익명함수를 사용함
```Kotlin
package techtown.org.fastcampus

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.TextView
import kotlinx.android.synthetic.main.activity_listener.* // xml을 직접 import함 gradle 설정을 해야함 kotlin-android-extensions를 직접 plugin 해야함

class Listener : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_listener)


        // 뷰를 activity로 가져오는 방법
        // 1> 직접 찾아서 가져온다
//        val textView : TextView = findViewById(R.id.hello) // findViewById id가 hello인 것 중 TextView인 것을 가져옴
        // 2> xml을 import해서 가져온다
//        hello.

    }
}
```

- 실습
```Kotlin
package techtown.org.fastcampus

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.util.Log
import android.view.View
import android.widget.TextView
import kotlinx.android.synthetic.main.activity_listener.* // xml을 직접 import함 gradle 설정을 해야함 kotlin-android-extensions를 직접 plugin 해야함

class Listener : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_listener)


        // 익명함수
        // 1 -> 람다 방식
       hello.setOnClickListener{ // onClick -> 사용자가 클릭했을 때, Listener -> 누를 경우 해당 부분이 호출됨, 안드로이드 OS가 Listener에게 알려줌(클릭시), 클릭된 뷰에 넘겨줌 해당 리스너를
            Log.d("click","Click!!")
        }

        // 2 -> 익명 함수 방식
        hello.setOnClickListener(object : View.OnClickListener {
            override fun onClick(p0: View?) {
                Log.d("click","Click!!")
            }
        })

        // 3 -> 이름이 필요한 경우(click)
        val click = object : View.OnClickListener{ // 인터페이스 만들 때 object를 만들고 바로 구현부 아래와 같이 작성함
            override fun onClick(p0: View?) { // onClick은 인터페이스임, 해당 부분을 구현하기 위해서 본문 작성필요 override를 함, 내용 작성
                Log.d("click","Click!!")
            }
        }

        hello.setOnClickListener(click)

        // 기존의 3의 방식에서 2의 익명함수 방식에서 최종적으로 람다방식으로 씀
    }
}
```