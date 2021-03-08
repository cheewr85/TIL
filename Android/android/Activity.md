## Activity
- 앱의 한 화면임 
- Life Cycle(생명주기)
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3646e0c9-28c6-4298-89c6-b4e733659804/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210308%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210308T075218Z&X-Amz-Expires=86400&X-Amz-Signature=febfe999fc0709e20eff3575b16f9f12573772a6c27bbcefef4172b167837534&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

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
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3dd192e8-2621-408a-a1e0-443d5cfe2004/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210308%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210308T075858Z&X-Amz-Expires=86400&X-Amz-Signature=fe58cac049c33c9a14eeb253fd64003511360af46eda298f3702f7541d732bcc&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 종료시키지 않고 홈으로 나오는 버튼을 누르면 아래와 같은 상태(onStop 찍히려면 onPause 거쳐야함), onPause와 onStop을 구분하기 힘듬,그래서 둘 중 한 곳에 작업을 함, 반드시 보장되는 것은 아님, 끄면 onDestroy처리됨
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f795b3d8-a4ab-4f41-bdb9-48ada1e91184/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210308%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210308T080004Z&X-Amz-Expires=86400&X-Amz-Signature=c5004575addaee2375f0b5aef0c352f75eb04ef9639568d18a0d7b32b3a5d135&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- 다시 실행시키면 onStart, onResume이 나옴(onRestart 생략됨)
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1c904fe4-8e13-4d5e-8ad7-24cf71a5d597/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210308%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210308T080031Z&X-Amz-Expires=86400&X-Amz-Signature=47e65881734cbc85540f02b88691f1cbea6e88d6f8ee1de49f3cc79978330254&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">
