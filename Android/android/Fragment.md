## Fragment
- Activity -> 앱에 보이는 한 화면의 단위

- Activity가 가지고 있는 문제
	- ex)
	- Activity가 길어지게 되면(파트 1,2,3,4,5,6) -> 관리 포인트가 많아진다 -> 관리가 어려워진다

- 다양한 디바이스에서 오는 문제
	- ex)
	- 안드로이드 디바이스가 너무 다양하다
	- 안드로이드에는 핸드폰만 있는게 아니다! -> 태블릿이 있다!

- 사용처
	- 액티비티의 파트를 나누어서 책임진다

- Fragment
	- 라이프 사이클이 존재한다
	- 액티비티 종속적이다

- 사용방법
	- XML에 ViewComponent로 추가한다
	- 코드로(동적)으로 추가한다

- 데이터 전달 방법
	- Activity -> Fragment : argument와 bundle 
	- Fragement -> Activity : 자체구현(리스너 구현)

### 실습
- Fragment로 넘기기 위해서 아래와 같이 fragment 태그를 활용함, 그리고 name을 통해 통제할 파일을 설정함, id도 반드시 지정해줘야함, 그러면 아래와 같이 fragment부분 FragmentOne.kt의 제어를 통해서 View를 컨트롤 할 수 있음
![one](/img/Android/android/Fragment/one.png)

- 그리고 아래와 같이 해당 메소드를 통해서 Fragment에 대한 레이아웃을 만들어 해당 레이아웃을 활용함
![two](/img/Android/android/Fragment/two.png)

- Logcat을 통해서 라이프 사이클을 보면 아래처럼 됨을 알 수 있음
- 라이프 사이클이 꽤 복잡해지는 경향이 있긴함
![three](/img/Android/android/Fragment/three.png)

- 프래그먼트는 Manifest에 추가되지 않음
- Fragment를 xml말고 코드로 추가할 수 있음
- Fragment를 container라는 id를 가진 레이아웃에 넣게끔 할 수 있음
- 여기서 Fragment를 붙일려면 부모뷰가 될 수 있는 레이아웃이어야 함
![four](/img/Android/android/Fragment/four.png)
![five](/img/Android/android/Fragment/five.png)

- 버튼을 누르면 화면이 바뀜
![six](/img/Android/android/Fragment/six.png)

- 아래와 같이 작용하게 하기 위해서 fragmentTransaction을 활용함
![seven](/img/Android/android/Fragment/seven.png)

- 하지만 위의 예시처럼 Fragment를 생성할 경우 Button에서만 있는 지역변수이기 때문에 detach가 원활하게 되지 않음 그러므로 아래와 같이 onCreate에 있는 변수로 설정을 해야 다 쓸 수 있음
![eight](/img/Android/android/Fragment/eight.png)

- 여기서 detach를 하고 다시 나와라 버튼을 눌러도 다시 붙지 않음, 그렇게 하기 위해선 remove를 써야함, 하지만 프래그먼트를 떼고 붙이는 일은 거의 하지 않기 때문에 필요할 때 사라지게 하므로 구분을 하는 경우는 흔하지 않음

- 프래그먼트에서 데이터를 넘겨주기 위해서 bundle을 통해서 넘기고 이를 argument를 통해서 넘겨줌
![nine](/img/Android/android/Fragment/nine.png)

- 이를 받을 때 아래와 같이 받음
![ten](/img/Android/android/Fragment/ten.png)
![eleven](/img/Android/android/Fragment/eleven.png)

- 프래그먼트에서 액티비티로 데이터를 보내는 법
- 이를 위해선 자체구현 아래와 같이 리스너를 직접 구현하기 위해 인터페이스를 구현함
```Kotlin
package techtown.org.fastcampus

import android.content.Context
import android.os.Bundle
import android.util.Log
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import androidx.fragment.app.Fragment
import kotlinx.android.synthetic.main.fragment_one.*


class FragmentOne:Fragment(){

    // 리스너 인터페이스 정의(꼭 이 클래스에 있을 필요는 없음)
   interface OnDataPassListener{
        fun onDataPass(data : String?)
    }
    // 바로 초기화를 늦추기 위해 late을 붙임
    lateinit var dataPassListener : OnDataPassListener

    override fun onAttach(context: Context) {
        Log.d("life_cycle","F onAttach")
        super.onAttach(context)
        dataPassListener = context as OnDataPassListener
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        Log.d("life_cycle","F onCreate")
        super.onCreate(savedInstanceState)
    }

    override fun onCreateView(
        inflater: LayoutInflater,
        container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        Log.d("life_cycle","F onCreateView")
        // 프래그먼트가 인터페이스를 처음으로 그릴 때 호출됨
        // inflater -> 뷰를 그려주는 역할
        // container -> 부모뷰
        return inflater.inflate(R.layout.fragment_one,container,false)
    }

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        Log.d("life_cycle","F onViewCreated")
        super.onViewCreated(view, savedInstanceState)

        // Activity의 Oncreate에서 했던 작업을 여기에서 한다
        pass.setOnClickListener{
           dataPassListener.onDataPass("Good bye")
        }
    }

    override fun onActivityCreated(savedInstanceState: Bundle?) {
        Log.d("life_cycle","F onActivityCreated")

        val data = arguments?.getString("hello")
        if (data != null) {
            Log.d("data", data)
        }

        super.onActivityCreated(savedInstanceState)
    }

    override fun onStart() {
        Log.d("life_cycle","F onStart")
        super.onStart()
    }

    override fun onResume() {
        Log.d("life_cycle","F onResume")
        super.onResume()
    }

    override fun onPause() {
        Log.d("life_cycle","F onPause")
        super.onPause()
    }

    override fun onStop() {
        Log.d("life_cycle","F onStop")
        super.onStop()
    }

    override fun onDestroyView() {
        Log.d("life_cycle","F onDestroyView")
        super.onDestroyView()
    }

    override fun onDetach() {
        Log.d("life_cycle","F onDetach")
        super.onDetach()
    }
}
```
```Kotlin
class FragmentActivity : AppCompatActivity(), FragmentOne.OnDataPassListener {
    // 해당 인터페이스를 implement했고 해당 리스너를 구현해줘야 하기때문에 참조함, 내용이 없기 때문에 반드시 구현해줘야함
    override fun onDataPass(data: String?) { // 데이터를 받음
        Log.d("pass", ""+ data)
    }
```