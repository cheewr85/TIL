## Intent
- 의도, 요구, 의사전달, 요청
- Intent의 사용처
	- Activity와 Activity
	- Android System과 내 App(전화)
	- 다른 App과 내 App -> 무작정 사용할 수 없음, 상호합의가 있어야 함
- 요청의 종류
	- 전달만 하는 요청
	- 리턴을 받는 요청
- Context
	- 문맥
	- 액티비티가 가지고 있느 주변 정보
```Kotlin
package techtown.org.fastcampus

import android.content.Intent
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import kotlinx.android.synthetic.main.activity_intent.*

class Intent1 : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_intent)

        change_activity.setOnClickListener{
            // 요청을 만듬 1 -> 2로 넘어가게끔
            val intent = Intent(this@Intent1, Intent2::class.java)  // packageContext 상에서 this를 쓰게 되면 현재 activity를 나타냄, Intent2에서 class.java를 넣어줘야함
            // this와 this@Intent1은 똑같은 기능을 하지만 @ 이하 부분은 좀 더 명확하게 나타내주는 부분임, 습관들이는게 좋음
            startActivity(intent)
        }
    }
}
```

- 인텐트를 통한 값 넘기기
```Kotlin
package techtown.org.fastcampus

import android.content.Intent
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import kotlinx.android.synthetic.main.activity_intent.*

class Intent1 : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_intent)

        change_activity.setOnClickListener{
            // 요청을 만듬 1 -> 2로 넘어가게끔
            val intent = Intent(this@Intent1, Intent2::class.java)  // packageContext 상에서 this를 쓰게 되면 현재 activity를 나타냄, Intent2에서 class.java를 넣어줘야함
            // this와 this@Intent1은 똑같은 기능을 하지만 @ 이하 부분은 좀 더 명확하게 나타내주는 부분임, 습관들이는게 좋음

            // Key, Value 방식 -> Key와 Value를 쌍으로 만들어 저장함.(dictionary 방식)
            intent.putExtra("number1",1) // 정보를 담아서 보내는 방법
            intent.putExtra("number2",2)
            startActivity(intent)

            // 똑같은 방식이지만 apply가 다름
            val intent2 = Intent(this@Intent1, Intent2::class.java)
            // this 키워드를 사용해서 intent를 씀 즉 여기서 this는 intent2임, 이 코드를 통해서 intent2의 putExtra 했을 때 작업을 한 눈에 알아볼 수 있음
            // apply를 통해 intent의 작업을 다 내포하고 있음을 알 수 있음
            intent2.apply{
                this.putExtra("number1",1)
                this.putExtra("number2",1)
            }
            startActivity(intent2)
        }
    }
}
```
```Kotlin
package techtown.org.fastcampus

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.util.Log

class Intent2 : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_intent2)

        // 보낸 값을 꺼내기 위해서, 꺼낼 때는 타입을 적어줘야함
        // crash 방지를 위해서 default값을 받아옴, 만일 값을 정상적으로 받지 않았을 경우
        val number1 = intent.getIntExtra("number1", 0)
        val number2 = intent.getIntExtra("number2", 0)

        Log.d("number", ""+number1)
        Log.d("number", ""+number2)
    }
}
```

- 요청에 대한 응답을 받는 처리
```Kotlin
package techtown.org.fastcampus

import android.content.Intent
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.util.Log
import kotlinx.android.synthetic.main.activity_intent.*

class Intent1 : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_intent)

        change_activity.setOnClickListener{
//            // 요청을 만듬 1 -> 2로 넘어가게끔
//            val intent = Intent(this@Intent1, Intent2::class.java)  // packageContext 상에서 this를 쓰게 되면 현재 activity를 나타냄, Intent2에서 class.java를 넣어줘야함
//            // this와 this@Intent1은 똑같은 기능을 하지만 @ 이하 부분은 좀 더 명확하게 나타내주는 부분임, 습관들이는게 좋음
//
//            // Key, Value 방식 -> Key와 Value를 쌍으로 만들어 저장함.(dictionary 방식)
//            intent.putExtra("number1",1) // 정보를 담아서 보내는 방법
//            intent.putExtra("number2",2)
//            startActivity(intent) // 전달만 하는 요청이므로 이 함수로는 보낸 결과값을 받을 수 없음

            // 똑같은 방식이지만 apply가 다름
            val intent2 = Intent(this@Intent1, Intent2::class.java)
            // this 키워드를 사용해서 intent를 씀 즉 여기서 this는 intent2임, 이 코드를 통해서 intent2의 putExtra 했을 때 작업을 한 눈에 알아볼 수 있음
            // apply를 통해 intent의 작업을 다 내포하고 있음을 알 수 있음(유지보수를 통해서 편함)
            intent2.apply{
                this.putExtra("number1",1)
                this.putExtra("number2",1)
            }
            // intent2에 여러개의 intent가 요청을 할 수 있음 이를 구분하기 위해서 requestCode를 사용함, 200이라는 requestCode로 Intent2를 Intent1 Activity가 Intent2 Activity로 보냄
            // requestCode를 활용하여 보냈을 때 다시 돌아왔을 때도 내가 보낸것이 맞는지 확인할 수 있음, Intent2에 보낸 것이
            startActivityForResult(intent2,200)
        }
    }

    // Intent2에서 보낸 결과 값을 받기 위해서 함수 override 해야함
    override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) { // resultCode는 Intent2에서 RESULT_OK의 코드값이고 data는 Intent2에서 resultIntent임

        // Intent2로 보낸 것이 맞는지 확인하고 그 보낸것을 바탕으로 값을 받음
        if(requestCode == 200){
            Log.d("number", ""+requestCode)
            Log.d("number", ""+resultCode)
            val result = data?.getIntExtra("result",0)
            Log.d("number",""+result)
        }

        super.onActivityResult(requestCode, resultCode, data)
    }
}
```
```Kotlin
package techtown.org.fastcampus

import android.app.Activity
import android.content.Intent
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.util.Log
import kotlinx.android.synthetic.main.activity_intent2.*

class Intent2 : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_intent2)



        result.setOnClickListener{
            // 보낸 값을 꺼내기 위해서, 꺼낼 때는 타입을 적어줘야함
            // crash 방지를 위해서 default값을 받아옴, 만일 값을 정상적으로 받지 않았을 경우
            val number1 = intent.getIntExtra("number1", 0)
            val number2 = intent.getIntExtra("number2", 0)

            Log.d("number", ""+number1)
            Log.d("number", ""+number2)

            // 값을 다시 전송시킴
            val result = number1 + number2

            val resultIntent = Intent()
            resultIntent.putExtra("result",result)
            // resultCode를 보냄 숫자를 넣어도 되지만 문자로 처리하는것도 좋음
            setResult(Activity.RESULT_OK, resultIntent) // 결과값을 돌려줌
            finish() // -> Activity 종료시킴


            // Stack
            // Intent2 -> 종료
            // Intent1             Intent1
        }
    }
}
```

- 암시적 인텐트
```Kotlin
package techtown.org.fastcampus

import android.content.Intent
import android.net.Uri
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.util.Log
import kotlinx.android.synthetic.main.activity_intent.*

class Intent1 : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_intent)

        change_activity.setOnClickListener{
//            // 요청을 만듬 1 -> 2로 넘어가게끔
//            val intent = Intent(this@Intent1, Intent2::class.java)  // packageContext 상에서 this를 쓰게 되면 현재 activity를 나타냄, Intent2에서 class.java를 넣어줘야함
//            // this와 this@Intent1은 똑같은 기능을 하지만 @ 이하 부분은 좀 더 명확하게 나타내주는 부분임, 습관들이는게 좋음
//
//            // Key, Value 방식 -> Key와 Value를 쌍으로 만들어 저장함.(dictionary 방식)
//            intent.putExtra("number1",1) // 정보를 담아서 보내는 방법
//            intent.putExtra("number2",2)
//            startActivity(intent) // 전달만 하는 요청이므로 이 함수로는 보낸 결과값을 받을 수 없음

//            // 똑같은 방식이지만 apply가 다름
//            val intent2 = Intent(this@Intent1, Intent2::class.java)
//            // this 키워드를 사용해서 intent를 씀 즉 여기서 this는 intent2임, 이 코드를 통해서 intent2의 putExtra 했을 때 작업을 한 눈에 알아볼 수 있음
//            // apply를 통해 intent의 작업을 다 내포하고 있음을 알 수 있음(유지보수를 통해서 편함)
//            intent2.apply{
//                this.putExtra("number1",1)
//                this.putExtra("number2",1)
//            }
//            // intent2에 여러개의 intent가 요청을 할 수 있음 이를 구분하기 위해서 requestCode를 사용함, 200이라는 requestCode로 Intent2를 Intent1 Activity가 Intent2 Activity로 보냄
//            // requestCode를 활용하여 보냈을 때 다시 돌아왔을 때도 내가 보낸것이 맞는지 확인할 수 있음, Intent2에 보낸 것이
//            startActivityForResult(intent2,200)
//        }
            // 암시적 인텐트, 이 예시를 보면 Uri parse에서 인터넷을 열 수 있는 브라우저에게 모두 요청해서 사용자가 선택함
            // 어떤 대상을 명시적 인텐트처럼 적는것이 아니라 행동을 적어서 할 수 있는 대상에게 모두 요청하여 선택함(+전화걸기 앱등)
            val intent = Intent(Intent.ACTION_VIEW, Uri.parse("http://m.naver.com"))
            startActivity(intent)
    }

    // Intent2에서 보낸 결과 값을 받기 위해서 함수 override 해야함
    override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) { // resultCode는 Intent2에서 RESULT_OK의 코드값이고 data는 Intent2에서 resultIntent임

        // Intent2로 보낸 것이 맞는지 확인하고 그 보낸것을 바탕으로 값을 받음
        if(requestCode == 200){
            Log.d("number", ""+requestCode)
            Log.d("number", ""+resultCode)
            val result = data?.getIntExtra("result",0)
            Log.d("number",""+result)
        }

        super.onActivityResult(requestCode, resultCode, data)
    }
}
```
```Kotlin
package techtown.org.fastcampus

import android.app.Activity
import android.content.Intent
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.util.Log
import kotlinx.android.synthetic.main.activity_intent2.*

class Intent2 : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_intent2)



        result.setOnClickListener{
            // 보낸 값을 꺼내기 위해서, 꺼낼 때는 타입을 적어줘야함
            // crash 방지를 위해서 default값을 받아옴, 만일 값을 정상적으로 받지 않았을 경우
            val number1 = intent.getIntExtra("number1", 0)
            val number2 = intent.getIntExtra("number2", 0)

            Log.d("number", ""+number1)
            Log.d("number", ""+number2)

            // 값을 다시 전송시킴
            val result = number1 + number2

            val resultIntent = Intent()
            resultIntent.putExtra("result",result)
            // resultCode를 보냄 숫자를 넣어도 되지만 문자로 처리하는것도 좋음
            setResult(Activity.RESULT_OK, resultIntent) // 결과값을 돌려줌
            finish() // -> Activity 종료시킴


            // Stack
            // Intent2 -> 종료
            // Intent1             Intent1
        }
    }
}
```