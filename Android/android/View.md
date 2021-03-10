## View 조작
- 정적인 뷰를 그릴 때는 XML을 활용하고 XML에서 쓰는 뷰를 동적으로 바꾸고 싶을 때는 Activity에서 그 뷰를 가져와 바꿔줄 수 있음 
- 리스너는 매우 다양한 종류가 있어서 활용할 수 있음
```Kotlin
package techtown.org.fastcampus

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.util.Log
import android.view.View
import android.widget.TextView
import kotlinx.android.synthetic.main.activity_listener.* // xml을 직접 import함 gradle 설정을 해야함 kotlin-android-extensions를 직접 plugin 해야함

class Listener : AppCompatActivity() {
    var number = 10
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
                hello.setText("안녕하세요")
                image.setImageResource(R.drawable.dog)
                number+=10
                Log.d("number","" + number) // 로그에 찍을 때 "" + 하면 자동으로 String으로 캐스팅됨
            }
        }

        hello.setOnClickListener(click)
        // 기존의 3의 방식에서 2의 익명함수 방식에서 최종적으로 람다방식으로 씀

        // 뷰를 조작하는 함수들
        // 1> setText
        // 2> setImageResource

        

    }
}
```