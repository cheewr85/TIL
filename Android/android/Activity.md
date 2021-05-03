## Activity
- 앱의 한 화면임 
- Life Cycle(생명주기)
![one](./img/Android/android/Activity/one.png)

- 콜백 -> 특정 동작 발생시 그 동작을 알 수 있게함 
- Activity 수명주기 참조(위와 같은 흐름으로 실행됨)
- onPause(), onStop()이 다시 불릴 수 있음, 여기서 다시 돌아올 때 onResume()은 반드시 돌아오게 되어 있음 
- App process killed -> 비정상적인 실행을 통해 충돌이 일어나면 다시 앱을 실행하므로 그 때 onCreate()가 실행됨
- onCreate
	- Activity가 만들어질 때 단 한 번만 호출됨 
	- Activity를 만들때 단 한 번만 하면 되는 작업들을 여기에서 해줌 
- onStart
- onResume
	- 다시 앱으로 돌아올 때 무조건 호출됨 
	- Activity가 다시 호출될 때 하면 되는 작업들을 여기에서 해줌 
- onPause
	- 화면의 일부가 가려졌을 때
- onStop
	- 화면 전부가 보이지 않을 때
- onDestroy

### 실습
```Kotlin
package techtown.org.fastcampus

import android.os.Bundle
import android.util.Log
import androidx.appcompat.app.AppCompatActivity

class MainActivity : AppCompatActivity() { // MainActivity가 AppCompatActivity를 상속받음
    override fun onCreate(savedInstanceState: Bundle?) { // onCreate라는 함수를 override라고 하고 savedInstanceState에서 Bundle 타입을 받음
        super.onCreate(savedInstanceState) // super는 AppCompatActivity를 의미함, 그 onCreate함수에 savedInstanceState를 넣어줌
        setContentView(R.layout.activity_main) // 화면을 그려주는 부분 layout을 넣어서 할당시킴

        // 기록을 남기기 위해 Log 사용함
        Log.d("life_cycle","onCreate")
    } // 단 한 번만 할 작업이 있음, 액티비티가 레이아웃을 그리는것은 한 번만 그려주면 되므로 한 번만 그리면 됨 그래서 onCreate에 있음


    override fun onStart() {
        super.onStart()
        Log.d("life_cycle","onStart")
    }

    override fun onResume() {
        super.onResume()
        Log.d("life_cycle","onResume")
    }

    override fun onPause() {
        super.onPause()
        Log.d("life_cycle","onPause")
    }

    override fun onStop() {
        super.onStop()
        Log.d("life_cycle","onStop")
    }

    override fun onDestroy() {
        super.onDestroy()
        Log.d("life_cycle","onDestroy")
    }
}
```

- 로그를 찍어서 확인가능(Activity running 상태)
![two](./img/Android/android/Activity/two.png)

- 종료시키지 않고 홈으로 나오는 버튼을 누르면 아래와 같은 상태(onStop 찍히려면 onPause 거쳐야함), onPause와 onStop을 구분하기 힘듬,그래서 둘 중 한 곳에 작업을 함, 반드시 보장되는 것은 아님, 끄면 onDestroy처리됨
![three](./img/Android/android/Activity/three.png)

- 다시 실행시키면 onStart, onResume이 나옴(onRestart 생략됨)
![four](./img/Android/android/Activity/four.png)
