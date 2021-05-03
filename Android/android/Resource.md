## Resource
- res 폴더 밑의 있는 내용
- color.xml
	- color값을 미리 설정해주어서 해당 color값을 저장해둠, 이렇게 되면 만일 디자인 변경 시 color를 바꿔야 하는 경우에 미리 저장해 둔 color를 통해서 그 값만 바꿔줄 수 있으므로 관리하기 편함
![one](./img/Android/android/Resource/one.png)

- string.xml
	- 이와 유사하게 만일 text 값을 설정했다가 수정하는 경우 간편학게 수정할 수 있게끔 values의 따로 두어서 저장함
![two](./img/Android/android/Resource/two.png)


- themes
	- style을 직접 설정해서 만들 수 있음, 앱 가동시 최상위에 뜨는 Bar등의 설정, 수정 후 Manifest에서 Theme 변경 가능함
	- 특정 상황을 제외하고는 많이 건드리지 않음

### 실습
- 코드를 통해서 설정 가능
```Kotlin
package techtown.org.fastcampus

import android.os.Build
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.util.Log
import kotlinx.android.synthetic.main.activity_resource.*

class resource : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_resource)

        // 1
        val ment = resources.getString(R.string.hello)
        Log.d("mentt","ment : " + ment)

        // 2
        val ment2 = getString(R.string.hello)
        Log.d("ment","ment : " + ment2)

        // SDK 버전에 따른 분기 처리
        val color = if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
            button.setBackgroundColor(getColor(R.color.textview_color))
        } else { // 낮은 버전의 경우 resource.을 활용해야함
            button.setBackgroundColor(resources.getColor(R.color.textview_color))
        }
        Log.d("mentt","ment : " + color)
        


    }
}
```