## Context
- 역할
	- ActivityManagerService(개발하기 편하도록 미리 구현 해놓은 기능)에 접근하도록 해주는 역할
	- 주변정보
- 안드로이드는 이미 많은 부분들이 만들어져있다 -> 이런것들을 사용하기 위해서는 Context가 필요한 경우가 많다
- 종류
	- activity의 context(주변정보) -> Activity의 주변정보(AndroidManifest에서 activity 태그)
	- application의 context(주변정보) -> Activity의 주변정보(AndroidManifest에서 application 태그)
	- ApplicationContext > ActivityContext, 즉 application이 더 넓은 포함관계를 가지고 있음
- 코드
```Kotlin
package techtown.org.fastcampus

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle

class Context : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_context)

        val context : Context = this // 자식은 부모의 타입이 될 수 있으므로 Context를 쓸 수 있음

        val applicationContext  = getApplicationContext()
    }
}
```