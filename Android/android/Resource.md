## Resource
- res 폴더 밑의 있는 내용
- color.xml
	- color값을 미리 설정해주어서 해당 color값을 저장해둠, 이렇게 되면 만일 디자인 변경 시 color를 바꿔야 하는 경우에 미리 저장해 둔 color를 통해서 그 값만 바꿔줄 수 있으므로 관리하기 편함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3ef5bc85-ead2-4945-ab3a-afb7ae940778/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210326%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210326T042033Z&X-Amz-Expires=86400&X-Amz-Signature=cde3eedc73880a91a0cf7765253bc1bc42faf01254d75286776b7f45effc25d6&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

- string.xml
	- 이와 유사하게 만일 text 값을 설정했다가 수정하는 경우 간편학게 수정할 수 있게끔 values의 따로 두어서 저장함
<img src="https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0505c526-0032-4322-bdeb-124a131279b8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210326%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210326T042108Z&X-Amz-Expires=86400&X-Amz-Signature=83dd32a5f8024edd7e1675d497fd1283849f58196398a0a27dc85685df05c644&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22">

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