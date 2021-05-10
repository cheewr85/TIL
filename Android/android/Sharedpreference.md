## Sharedpreference
- 데이터베이스
	- 데이터를 저장하기 위함
- 데이터 저장 방식
	- RDB (Relational DataBase)
		- 관계형 데이터베이스
		- 엑셀처럼 생김
			|이름|학번|학교|성별|
			|----|----|----|----|
       		|홍길동|1|서울|남|
        	|김진짜|2|전북|여|

- Key-Value
    - 쌍으로 저장하는 방식 (key, value), 검색속도가 매우 빠름

- RDBMS
    - Relational Database Management System
    - RDB를 관리하기 위한 툴
    - MySQL
    - Oracle
    - PostgreSQL
- SQL
    - RDBMS를 위한 언어이다

- NoSQL
    - SQL말고 다르게 해보자!

안드로이드 데이터베이스
- SQLiteDatabase
- SharedPreference
    - Key-Value 방식
    - 목적 : 공유된 사용자의 기호 방식
    - 하드하게 데이터베이스 시스템을 구축할 수 없다!

- 실습
- 데이터를 지우기 위해서는 설정에 들어가서 앱에 있는 데이터를 지우면 됨

```kotlin
package techtown.org.fastcampus

import android.content.SharedPreferences
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.util.Log
import kotlinx.android.synthetic.main.activity_shared_preference.*

class SharedPreferenceActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_shared_preference)

        // SharedPreference에 저장하는 방법
        val sharedPreference = getSharedPreferences("sp1",MODE_PRIVATE) // name과 mode를 넣음, name은 sharedpreference를 각각 구분하기 위해서 만듬
        // Mode
        // - MODE_PRIVATE : 생성한 application에서만 사용 가능
        // - MODE_WORLD_READABLE : 다른 application에서 사용 가능 -> 읽을수만 있다
        // - MODE_WORLD_WRITEABLE : 다른 application에서 사용 가능 -> 기록도 가능
        // - MODE_MULTI_PROCESS : 이미 호출되어 사용중인지 체크
        // - MODE_APPEND : 기존 preference에 신규로 추가

        // 데이터를 넣기 위해서 에디터를 통해 데이터를 sharedpreference에 넣어줌
        val editor: SharedPreferences.Editor = sharedPreference.edit()
        editor.putString("hello","안녕하세요") // editor를 통해서 데이터를 설정함
        editor.commit() // 데이터를 넣기 위해서 커밋이 필요함

        // sp1 -> Sharedpreference, 갱신을 위해서는 맞는 preference를 참조해서 해야함함
       //        (Key,Value) -> ("hello", "안녕하세요")
        // sp2 -> Sharedpreference
        //        (Key,Value) -> ("hello", "안녕하세요11")

        button.setOnClickListener {
            // SharedPreference에 값을 불러오는 방법
            val sharedPreference = getSharedPreferences("sp1", MODE_PRIVATE)
            val value = sharedPreference.getString("hello","데이터 없음")
            Log.d("key-value", "Value : " + value)
        }
    }
}
```

- 코드상으로 sharedpreference 값을 지우는 법
```kotlin
package techtown.org.fastcampus

import android.content.SharedPreferences
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.util.Log
import kotlinx.android.synthetic.main.activity_shared_preference.*

class SharedPreferenceActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_shared_preference)

        // SharedPreference에 저장하는 방법

        // Mode
        // - MODE_PRIVATE : 생성한 application에서만 사용 가능
        // - MODE_WORLD_READABLE : 다른 application에서 사용 가능 -> 읽을수만 있다
        // - MODE_WORLD_WRITEABLE : 다른 application에서 사용 가능 -> 기록도 가능
        // - MODE_MULTI_PROCESS : 이미 호출되어 사용중인지 체크
        // - MODE_APPEND : 기존 preference에 신규로 추가

        // sp1 -> Sharedpreference, 갱신을 위해서는 맞는 preference를 참조해서 해야함함
       //        (Key,Value) -> ("hello", "안녕하세요")
        // sp2 -> Sharedpreference
        //        (Key,Value) -> ("hello", "안녕하세요11")

        save_btn.setOnClickListener{
            // 데이터를 넣기 위해서 에디터를 통해 데이터를 sharedpreference에 넣어줌
            val sharedPreference = getSharedPreferences("sp1",MODE_PRIVATE) // name과 mode를 넣음, name은 sharedpreference를 각각 구분하기 위해서 만듬
            val editor: SharedPreferences.Editor = sharedPreference.edit()
            editor.putString("hello","안녕하세요") // editor를 통해서 데이터를 설정함
            editor.putString("goodbye","안녕히 가세요")
            editor.commit() // 데이터를 넣기 위해서 커밋이 필요함
        }

        load_button.setOnClickListener {
            // SharedPreference에 값을 불러오는 방법
            val sharedPreference = getSharedPreferences("sp1", MODE_PRIVATE)
            val value1 = sharedPreference.getString("hello","데이터 없음1")
            val value2 = sharedPreference.getString("goodbye","데이터 없음2")
            Log.d("key-value", "Value 1 : " + value1)
            Log.d("key-value", "Value 2 : " + value2)
        }

        delete_button.setOnClickListener{
            val sharedPreference = getSharedPreferences("sp1",MODE_PRIVATE) // name과 mode를 넣음, name은 sharedpreference를 각각 구분하기 위해서 만듬
            val editor = sharedPreference.edit()
            editor.remove("hello") // 해당 키값만 없앰, 특정 키-value만 없앰
            editor.commit()
        }

        delete_all_button.setOnClickListener{
            val sharedPreference = getSharedPreferences("sp1",MODE_PRIVATE) // name과 mode를 넣음, name은 sharedpreference를 각각 구분하기 위해서 만듬
            val editor = sharedPreference.edit()
            editor.clear() // 전부다 지워줌
            editor.commit()
        }
    }
}
```