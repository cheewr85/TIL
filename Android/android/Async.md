## Async
- 비동기 -> Async
- 동기 -> Sync

- 동기 방식
    - 작업을 순서대로 진행한다
    - A -> B -> C -> D
    - 위에서부터 아래로 실행

- 비동기 방식
    - 쓰레드(백그라운드)를 만들어서 작업을 따로 처리한다
```Markdown

                     결과를 받는다
---------------------------------------------------------->
         | | |  | | |
        -------------
            작업
```
- 안드로이드에서 Async 다루는 방법
    - AsyncTask 상속받는다
        - onPreExcute      : 쓰레드 출발하기전에 할 작업
        - doInBackground   : 쓰레드가 할 작업
        - onPregressUpdate : 중간중간에 MainThread로 온다
        - onPostExcute     : 작업을 다 마친후 MainThread

- Async의 장점
    - Main Thread를 기다리게 할 필요가 없다
    - 네트워크 작업, 비는 시간을 작업을 활용할 수 있음, Async를 사용하지 않으면 비는 시간 동안 아무것도 안하고 기다리기만 함

- Async의 단점
    - 재사용이 불가능하다, 한 번 만들어지고 사라진것을 또 쓸 수 없이 매번 다시 만들어야함
    - 구현된 Activity가 종료될 경우 따라서 종료되지 않는다, 자동으로 멈추지 않음, 다른 화면으로 넘어가도 계속 작업을 함
    - AsyncTask는 하나만 실행될 수 있다, 하나만 만들 수 있기 때문에 여러개를 만들어 동시에 실행시키면 하나가 다 돌고 또 다시 실행되는 반복작업이 된다(병렬처리가 안됨)

- 실습
```kotlin
package techtown.org.fastcampus

import android.os.AsyncTask
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.ProgressBar
import android.widget.TextView
import kotlinx.android.synthetic.main.activity_async.*

class AsyncActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_async)

        var task : BackgroundAsyncTask? = null
        start.setOnClickListener{
            task = BackgroundAsyncTask(progressbar, ment) // task를 만들고 xml에 정의한 progressbar와 textview를 넣음
            task?.execute()
        }

        stop.setOnClickListener{
            task?.cancel(true)
        }
    }
}

// AsyncTask를 만들어줌, 실행 누르면 퍼센티지가 차게끔 함
class BackgroundAsyncTask(
    val progressbar : ProgressBar,
    val progressText : TextView
): AsyncTask<Int, Int, Int>() {

    // params -> doInBackground에서 사용할 타입 -> 해당 타입에 맞춰서 params가 implements가 됨
    // progress -> onProgressUpdate에서 사용할 타입
    // result -> onPostExecute에서 사용할 타입
    var percent : Int = 0

    override fun onPreExecute() {
        percent = 0 // 작업이 실행되므로 0으로 시작
        progressbar.setProgress(percent) // 넘겨받은 매개변수 progressbar에서 시작하는 것이므로 0으로 세팅함
    }

    override fun doInBackground(vararg params: Int?): Int {  // vararg는 Int가 여러개 올 수 있음을 의미함
        while (isCancelled() == false) { // 작업이 취소되기 전까지 계속 작업을 함
            percent++
            if(percent>100) { // 작업이 끝나면 반복문 나감
                break
            } else { // 작업중인 경우 진행경과에 대해서 메인 스레드에 가지고 들어감 percent가 onProgressUpdate로 들어가게 됨
                publishProgress(percent)
            }
            try { // 일부러 스레드를 늦춤, 작업을 보기 위해서
                Thread.sleep(100)
            } catch (e: Exception){
                e.printStackTrace()
            }
        }
        return percent // 100퍼센트 됐을 때 100을 리턴해줌
   }

    // 매개변수로 받은 progressbar, progressText를 활용함
    override fun onProgressUpdate(vararg values: Int?) { // Int로 Async를 설정해서 오버라이드 시 values가 Int로 받음, String으로 보내면 String으로 받음
        // publishProgress를 통해서 그 값이 values로 들어옴
        progressbar.setProgress(values[0] ?: 0) // 그 values를 바탕으로 progress를 업데이트함, null 인 경우 0으로 체크함
        progressText.setText("퍼센트 : " + values[0]) // 해당 뷰를 갱신함
        super.onProgressUpdate(*values)
    }

    override fun onPostExecute(result: Int?) {  // Int로 Async를 설정해서 result 역시 Int로 받음
        progressText.setText("작업이 완료되었습니다")
    }

    override fun onCancelled() { // 취소를 누른 경우 초기화 시킴
        progressbar.setProgress(0)
        progressText.setText("작업이 취소되었습니다")
    }
}
```
- 실습2, 작업은 화면이 바뀌어도 계속 진행됨, 액티비티 라이프사이클에서 중간에 직접 종료를 시켜줘야함
```kotlin
package techtown.org.fastcampus

import android.content.Intent
import android.os.AsyncTask
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.ProgressBar
import android.widget.TextView
import kotlinx.android.synthetic.main.activity_async.*

class AsyncActivity : AppCompatActivity() {
    var task : BackgroundAsyncTask? = null
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_async)

        start.setOnClickListener{
            task = BackgroundAsyncTask(progressbar, ment) // task를 만들고 xml에 정의한 progressbar와 textview를 넣음
            task?.execute()
        }

        stop.setOnClickListener{
//            task?.cancel(true)
            startActivity(Intent(this,Intent2::class.java))
        }

    }
    override fun onPause() {
        task?.cancel(true)
        super.onPause()
    }

}

// AsyncTask를 만들어줌, 실행 누르면 퍼센티지가 차게끔 함
class BackgroundAsyncTask(
    val progressbar : ProgressBar,
    val progressText : TextView
): AsyncTask<Int, Int, Int>() {

    // params -> doInBackground에서 사용할 타입 -> 해당 타입에 맞춰서 params가 implements가 됨
    // progress -> onProgressUpdate에서 사용할 타입
    // result -> onPostExecute에서 사용할 타입
    var percent : Int = 0

    override fun onPreExecute() {
        percent = 0 // 작업이 실행되므로 0으로 시작
        progressbar.setProgress(percent) // 넘겨받은 매개변수 progressbar에서 시작하는 것이므로 0으로 세팅함
    }

    override fun doInBackground(vararg params: Int?): Int {  // vararg는 Int가 여러개 올 수 있음을 의미함
        while (isCancelled() == false) { // 작업이 취소되기 전까지 계속 작업을 함
            percent++
            if(percent>100) { // 작업이 끝나면 반복문 나감
                break
            } else { // 작업중인 경우 진행경과에 대해서 메인 스레드에 가지고 들어감 percent가 onProgressUpdate로 들어가게 됨
                publishProgress(percent)
            }
            try { // 일부러 스레드를 늦춤, 작업을 보기 위해서
                Thread.sleep(100)
            } catch (e: Exception){
                e.printStackTrace()
            }
        }
        return percent // 100퍼센트 됐을 때 100을 리턴해줌
   }

    // 매개변수로 받은 progressbar, progressText를 활용함
    override fun onProgressUpdate(vararg values: Int?) { // Int로 Async를 설정해서 오버라이드 시 values가 Int로 받음, String으로 보내면 String으로 받음
        // publishProgress를 통해서 그 값이 values로 들어옴
        progressbar.setProgress(values[0] ?: 0) // 그 values를 바탕으로 progress를 업데이트함, null 인 경우 0으로 체크함
        progressText.setText("퍼센트 : " + values[0]) // 해당 뷰를 갱신함
        super.onProgressUpdate(*values)
    }

    override fun onPostExecute(result: Int?) {  // Int로 Async를 설정해서 result 역시 Int로 받음
        progressText.setText("작업이 완료되었습니다")
    }

    override fun onCancelled() { // 취소를 누른 경우 초기화 시킴
        progressbar.setProgress(0)
        progressText.setText("작업이 취소되었습니다")
    }
}
```