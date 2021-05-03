## Thread
- 작업 흐름, 여러가지 흐름을 원하는대로 만들 수 있음
```MarkDown
앱 실행 ----> launcher Activity ----> ----> ----> 작업흐름

안드로이드의 쓰레드
-> MainThread
---------------------------------------------------------->
    -> launcher Activity
                        -> Activity B
                                     -> 영상재생
                                                -> 기타등등

할 일 : 더하기, 빼기, 곱하기, 나누기
MainThread만 있는 경우
---------------------------------------------------------->
더하기 -----------> 빼기 ---------> 곱하기 --------> 나누기


다른 쓰레드가 있는 경우 -> 여러가지 일을 한 번에 할 수 있다
---------------------------------------------------------->
              빼기
              ---------->
                     곱하기
                     ----------->
   더하기
   -------------------------------------->
                                   나누기
                                   -------------->
```
- 안드로이드 MainThread의 특징 
	- UI(User Interface) Thread
		- 사용자의 Input을 받는 스레드
	- 절대 정지시킬 수 없다!(앱이 끝날 때까지 계속 흘러감), 하면 안됨!
		- 왜냐하면, 정지시키거나 종료시키면 더 이상 사용자의 Input을 받을 수 없기 때문에

- 실습
```Kotlin
package techtown.org.fastcampus

import android.os.Build
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.util.Log
import androidx.annotation.RequiresApi
import kotlinx.android.synthetic.main.activity_thread.*

class ThreadActivity : AppCompatActivity() {
    @RequiresApi(Build.VERSION_CODES.M)
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_thread)



        val runnable : Runnable = object : Runnable {
            override fun run() {
                Log.d("thread-1","Thread1 is made")
            }
        }

        val thread : Thread = Thread(runnable) // Thread를 생성하고 Runnable을 생성함, 그리고 해당 Runnable을 Thread에 넣어서 실행시켜야함

        button.setOnClickListener{ // 버튼을 클릭시 스레드가 출발하게 함
            thread.start() // Therad가 runnable을 하는 것까지는 알지만 그 다음 실행하기 위해서 start함수가 필요함
        }

        // 아래와 같이 바로 스레드를 만들어서 쓸 수 있음
        // 람다를 사용하지 않은 방식
        Thread(object : Runnable {
            override fun run() {
                Log.d("thread-1","Thread2 is made")
            }

        }).start()
        // 람다방식
        Thread(Runnable{
            Thread.sleep(2000) // 스레드 실행후 2초 뒤에 나오게 함, 2초동안 잠재움
            Log.d("thread-1","Thread3 is made")
            // UiThread위에서 돌림(mainThread로 가서 처리)
            runOnUiThread {
            button.setBackgroundColor(getColor(R.color.textview_color)) // 다른 스레드에서 UI 부분에 접근하면 에러가 남, 하지만 이와같이 runOn에서는 정상작동됨
            }
        }).start()


    }
}
```
- 스레드 실행시 아래와 같이 바로 나타남
![one](./img/Android/android/Thread/one.png)
