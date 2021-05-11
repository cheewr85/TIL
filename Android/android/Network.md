## Network

- 네트워크
	- 통신

```markdown
DataBase <-----> Server <------> Client(app,web,....)
  글                                 A
  댓글                               B
```

- Local DataBase의 한계
	- 동기화가 어렵다
	- 상호작용이 불가능하다
	- 그러므로 Server와 통신함

- 서버와 통신하는 방법
	- 해당 url로 요청한다
	- 인증 정보를 보냄
	- JSON 형식을 사용해서 data를 보낸다
	- JavaScript Object Notation -> Javascript에서 객체를 만들 때 사용하는 표현식, 보편화 됨, 서버와 통신하기 위한 데이터 형식

- JSON 형식
	- [] -> List
	- {} -> 객체
    	-> "" -> 문자열
    	-> ""없으면 -> 숫자

```markdown
Json Response
[
    { -> List 0번째
        "id": 1, -> 타입이 뭔지 모름, JavaScript로 구분을 못하므로, 그래서 문서에 써있음, API를 통해서, 필드값, 필드의 의미가 문서에 써 있음
        "name": "홍길동",
        "age": 20,
        "intro": "나는 홍길동이다!"
    },
    { -> List 1번째
        "id": 2,
        "name": "김아무개",
        "age": 10,
        "intro": "난 김아무개 입니다 :)"
    }
]
```

- Json Parsing
	- JSON을 코틀린이나 자바가 이해할 수 있게 변형하는 과정

- Serializable(직렬화)
	- 자바 시스템 내부에서 사용되는 object를 외부에서 사용할 수 있도록 byte 형태로 데이터를 바꾸는 것
```markdown
------------------------>
  id, name, age, intro -> 꼬치에 끼듯이 하나로 묶어버림, 실제 사용할 때 하나씩 필요한 것을 빼서 씀
```

- 코틀린 / 자바가 이해할 수 있는 틀 -> 객체를 만들 때 class를 사용하므로 class를 통해서 하나씩 필요한 것을 씀
	- 하나씩 빼서 씀 키-value로 이루어짐 위에서 키에서 변수명과 같은 것을 찾아서 할당함 id 변수와 같은 키 id에서 1을 받음
	- 이를 다 넣어주면 해당 class는 constructor가 생성됨
```markdown
class Person(
    var id : Int? = null
    var name: String? = null
    var age: Int? = null
    var intro: String? = null
}
Person(1, "김아무개", 20, "안녕하세요") -> 기존의 class를 만들어서 생성자까지 만들어 선언한 것을 Serializable을 통해서 JSON을 받아서 생성자에 넣어주어 객체가 만들어지는 것
```

- Request Type                  Status Code
	- GET    -> 정보 요청        -> 200 OK
	- POST   -> 정보 추가 요청   -> 201 Created
	- DELETE -> 정보 삭제 요청
	- PUT    -> 정보 수정 요청

- Status Code
	- 200번대 -> 처리가 잘 됐다


- 실습
```kotlin
package techtown.org.fastcampus

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import java.io.BufferedReader
import java.io.InputStreamReader
import java.net.HttpURLConnection
import java.net.URL

class NetworkActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_network)

        val urlString: String = "http://mellowcode.org/json/students" // 요청할 urlString을 만듬
        val url : URL = URL(urlString) // 만든 urlString을 URL 객체로 만듬
        val connection : HttpURLConnection = url.openConnection() as HttpURLConnection // 받은 url을 열고 HttpURLConnection으로 캐스팅함

        connection.requestMethod ="GET" // request를 GET으로 받음, 정보를 받아옴
        connection.setRequestProperty("Content-Type","application/json") // 내가 보내는 속성을 적음, Content-Type이며 application/json임, 헤더 작성

        var buffer = ""
        if(connection.responseCode == HttpURLConnection.HTTP_OK) { // HttpURL이 정상적으로 처리되어 응답을 받았을 때
            val reader = BufferedReader( // 네트워크를 처리하는 방식인데 이 방식으로 처리하면 메인스레드에서 쓰기 때문에 멈춰버림, 즉 메인스레드에서 네트워크 처리를 하면 안되고 비동기 방식을 사용해야함
                InputStreamReader(
                    connection.inputStream,
                        "UTF-8"
                )
            )
            buffer = reader.readLine()
        }
    }
}
```

- AsyncTask 처리해서 네트워크 처리, Serializable로 파싱을 함, 만일 그렇게 하지 않으면 코틀린 문법을 활용해서 직접 하나하나 인덱스로 찾아서 만들어야 함
```kotlin
package techtown.org.fastcampus

import android.os.AsyncTask
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import java.io.BufferedReader
import java.io.InputStreamReader
import java.net.HttpURLConnection
import java.net.URL

class NetworkActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_network)

        NetworkTask().execute() // 네트워크 처리를 함

    }
}

class NetworkTask() : AsyncTask<Any?, Any?, Any?>() {
    // 네트워크 처리는 비동기 방식으로 처리해야 하므로 AsyncTask를 활용해서 처리하기 위해서 클래스를 새로 만듬
    override fun doInBackground(vararg params: Any?): Any? {
        val urlString: String = "http://mellowcode.org/json/students" // 요청할 urlString을 만듬
        val url : URL = URL(urlString) // 만든 urlString을 URL 객체로 만듬
        val connection : HttpURLConnection = url.openConnection() as HttpURLConnection // 받은 url을 열고 HttpURLConnection으로 캐스팅함

        connection.requestMethod ="GET" // request를 GET으로 받음, 정보를 받아옴
        connection.setRequestProperty("Content-Type","application/json") // 내가 보내는 속성을 적음, Content-Type이며 application/json임, 헤더 작성

        var buffer = ""
        if(connection.responseCode == HttpURLConnection.HTTP_OK) { // HttpURL이 정상적으로 처리되어 응답을 받았을 때
            val reader = BufferedReader( // buffered, 하나씩 읽는것이 아니라 한꺼번에 읽는다는 것
                    InputStreamReader( // inputstream을 읽는 것, 인터넷을 타고 넘어올 때 byte로 넘어가므로 아래와 같이 UTF-8 형식으로 읽겠다는 것임
                            connection.inputStream,
                            "UTF-8"
                    )
            )
            buffer = reader.readLine() // buffer를 읽어서 서버에 저장된 데이터를 받아서 readLine을 통해서 읽음, 그리고 읽은 내용을 객체로 넘겨야함 즉 파싱을 해야함, 변경과정이 필요
        }
        

        return null
    }

}
```

- 데이터를 받기 위한 클래스
```kotlin
package techtown.org.fastcampus

import java.io.Serializable

class PersonFromServer( // 네트워크로 통해 받은 buffer에 대해서 파싱을 하기 위해 만든 클래스
    var id : Int? = null,
    var name : String? = null,
    var age : Int? = null,
    var intro : String? = null
) : Serializable // 데이터를 사용하기 위해서 직렬화 즉, Serializable을 시킴, implements함
```

- 파싱한 내용을 받기 위해서 하나하나 인덱싱 처리를 해서 노가다로 받지 않게 하기 위해서 Gson을 사용함, 좀 더 편하게 틀을 주고 그 틀에 들어갈 수 있게 넣어줌, 그러면 Gson이 알아서 객체를 돌려줌, gson 라이브러리 추가
```kotlin
package techtown.org.fastcampus

import android.os.AsyncTask
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.util.Log
import com.google.gson.Gson
import java.io.BufferedReader
import java.io.InputStreamReader
import java.net.HttpURLConnection
import java.net.URL

class NetworkActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_network)

        NetworkTask().execute() // 네트워크 처리를 함

    }
}

class NetworkTask() : AsyncTask<Any?, Any?, Any?>() {
    // 네트워크 처리는 비동기 방식으로 처리해야 하므로 AsyncTask를 활용해서 처리하기 위해서 클래스를 새로 만듬
    override fun doInBackground(vararg params: Any?): Any? {
        val urlString: String = "http://mellowcode.org/json/students" // 요청할 urlString을 만듬
        val url : URL = URL(urlString) // 만든 urlString을 URL 객체로 만듬
        val connection : HttpURLConnection = url.openConnection() as HttpURLConnection // 받은 url을 열고 HttpURLConnection으로 캐스팅함

        connection.requestMethod ="GET" // request를 GET으로 받음, 정보를 받아옴
        connection.setRequestProperty("Content-Type","application/json") // 내가 보내는 속성을 적음, Content-Type이며 application/json임, 헤더 작성

        var buffer = ""
        if(connection.responseCode == HttpURLConnection.HTTP_OK) { // HttpURL이 정상적으로 처리되어 응답을 받았을 때
            val reader = BufferedReader( // buffered, 하나씩 읽는것이 아니라 한꺼번에 읽는다는 것
                    InputStreamReader( // inputstream을 읽는 것, 인터넷을 타고 넘어올 때 byte로 넘어가므로 아래와 같이 UTF-8 형식으로 읽겠다는 것임
                            connection.inputStream,
                            "UTF-8"
                    )
            )
            buffer = reader.readLine() // buffer를 읽어서 서버에 저장된 데이터를 받아서 readLine을 통해서 읽음, 그리고 읽은 내용을 객체로 넘겨야함 즉 파싱을 해야함, 변경과정이 필요
        }
        // Gson을 불러오고 받아온 buffer 데이터를 만들어든 PersonFromServer 클래스에 넣어주면 됨
        // 단 여기서 만든 PersonFromServer 클래스는 서버내의 id, name, age, intro의 객체를 받기 위한 클래스임
        // 그 전에 해당 객체는 List로 구성되어 있기 때문에 이를 아래와 같이 Array로 묶어서 받아줘야함
        val data = Gson().fromJson(buffer, Array<PersonFromServer>::class.java)
        val age = data[0].age // 그리고 받은 데이터를 가지고 array이기 때문에 이와 같이 써서 데이터를 확인할 수 있음
        Log.d("conn","age : " + age)

        return null
    }

}
```

- Profiler를 통해서 실제 메모리, CPU, 네트워크를 확인해서 정상적으로 받았는지에 대해서 확인할 수 있음
- 받은 데이터를 활용하여 View에 적용시키기 위한 실습, 리사이클러뷰의 적용
```kotlin
package techtown.org.fastcampus

import android.os.AsyncTask
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.util.Log
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import android.widget.TextView
import androidx.recyclerview.widget.LinearLayoutManager
import androidx.recyclerview.widget.RecyclerView
import com.google.gson.Gson
import kotlinx.android.synthetic.main.activity_network.*
import java.io.BufferedReader
import java.io.InputStreamReader
import java.net.HttpURLConnection
import java.net.URL

class NetworkActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_network)

        NetworkTask( // 아래와 같이 직접 활용할 요소들을 매개변수로 넣어서 적용시킴
            recycler_person,
            LayoutInflater.from(this@NetworkActivity)
        ).execute() // 네트워크 처리를 함

    }
}

class NetworkTask(
    val recyclerView: RecyclerView,
    val inflater: LayoutInflater // 네트워크로 데이터를 받은뒤 이를 리사이클러뷰에 바로 적용시키기 위해서 생성자로 받음
) : AsyncTask<Any?, Any?, Array<PersonFromServer>>() {
    override fun onPostExecute(result: Array<PersonFromServer>?) { // 메인 스레드에서 진행, UI에 접근이 가능함
        // UI에 접근해서 데이터를 그려줄 것이므로 타입을 Array이고 Server에서 받은 데이터로 받음
        // UI에 접근이 가능하므로 보여주기 위한 UI에 리사이클러뷰를 어댑터 설정하고 아래와 같이 활용함
        val adapter = PersonAdapter(result!!, inflater)
        recyclerView.adapter = adapter
        super.onPostExecute(result)
    }

    override fun doInBackground(vararg params: Any?): Array<PersonFromServer>? { // onPostExecute에 들어가기 위해서 Array의 형태로 바꿈, doIn에서 작업하고 PostExecute로 넘어가기 때문에
        val urlString: String = "http://mellowcode.org/json/students"
        val url : URL = URL(urlString)
        val connection : HttpURLConnection = url.openConnection() as HttpURLConnection

        connection.requestMethod ="GET"
        connection.setRequestProperty("Content-Type","application/json")

        var buffer = ""
        if(connection.responseCode == HttpURLConnection.HTTP_OK) {
            val reader = BufferedReader(
                    InputStreamReader(
                            connection.inputStream,
                            "UTF-8"
                    )
            )
            buffer = reader.readLine()
        }

        val data = Gson().fromJson(buffer, Array<PersonFromServer>::class.java)
        return data // doInBack에서 작업이 완료된 것이 onPost로 넘어가는데 여기서 넘어가는게 data가 넘어가기 때문에 data를 리턴함
    }
}

class PersonAdapter( // 리사이클러뷰를 사용하기 위해서 Adapter가 필요함
    val personList : Array<PersonFromServer>, // 서버를 통해 받은 Person을 personList 변수에 저장해서 리사이클러뷰에 사용할 것임
    val inflater : LayoutInflater
) : RecyclerView.Adapter<PersonAdapter.ViewHolder>() {

    inner class ViewHolder(itemView : View):RecyclerView.ViewHolder(itemView){ // 데이터를 적용하기 위해서 각각 데이터를 나타낼 뷰홀더 이너클래스 만듬
        val name : TextView
        val age : TextView
        val intro : TextView

        init { // 받은 뷰를 생성자를 통해서 적용시킬 뷰를 찾아서 설정함
            name = itemView.findViewById(R.id.person_name)
            age = itemView.findViewById(R.id.person_age)
            intro = itemView.findViewById(R.id.person_ment)
        }
    }

    override fun getItemCount(): Int {
        return personList.size
    }

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ViewHolder { // ViewHolder를 통해서 리사이클러뷰에 적용할 뷰를 찾아서 데이터에 연결시켜서 설정하고
        // 이제 그 연결시킨 뷰를 보여주기 위해서 해당 레이아웃을 찾아서 적용시킴
        val view = inflater.inflate(R.layout.person_list_item, parent, false)
        return ViewHolder(view)
    }

    override fun onBindViewHolder(holder: ViewHolder, position: Int) { // 서버를 통해 받은 데이터를 활용해서 holder에서 적용한 뷰에 적용함
        holder.name.setText(personList.get(position).name ?: "")
        holder.age.setText(personList.get(position).age.toString())
        holder.intro.setText(personList.get(position).intro ?: "")
    }

}
```
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".NetworkActivity">

    <!-- 코틀린 코드에서 설정할 레이아웃 매니저를 xml을 통해서 설정함 -->
    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/recycler_person"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:layoutManager="androidx.recyclerview.widget.LinearLayoutManager"
        />

</LinearLayout>
```

- 네트워크를 라이브러리를 통해서 AsyncTask를 사용하지 않고 쓸 수 있음
- Retrofit을 이용한 네트워크 통신, 원하는 데이터 타입으로 자동으로 변환해주게끔 함
```kotlin
implementation 'com.squareup.retrofit2:retrofit:2.9.0'
implementation 'com.squareup.retrofit2:converter-gson:2.9.0'
```

- Retrofit은 baseUrl을 기준으로 뒷부분 Url을 관리할 수 있게끔 구조적으로 도움을 줌
```kotlin
package techtown.org.fastcampus

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.util.Log
import retrofit2.Call
import retrofit2.Callback
import retrofit2.Response
import retrofit2.Retrofit
import retrofit2.converter.gson.GsonConverterFactory

class RetrofitActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_retrofit)

        // 빌더 패턴
        // http://mellowcode.org/json/students/
        // http://mellowcode.org/test/code/
        val retrofit = Retrofit.Builder()
            .baseUrl("http://mellowcode.org/") // 변하지 않는 부분을 baseUrl이라고 함
            .addConverterFactory(GsonConverterFactory.create()) // 등록한 converter를 통해서 Gson을 통해서 자동으로 객체를 뽑아서 쓸 수 있게 처리함
            .build()

        // 만들어둔 retrofitservice interface를 연결시켜줄 것임
        val service = retrofit.create(RetrofitService::class.java)

        // Retrofitservice에서 만든 함수를 통해서 받은 데이터를 콜백해서 받음
        service.getStudentsList().enqueue(object : Callback<ArrayList<PersonFromServer>>{ // enqueue로 해당 통신을 대기줄에 올려놓은것을 의미함
            override fun onFailure(call: Call<ArrayList<PersonFromServer>>, t: Throwable) { // 통신 실패했을 때
                Log.d("retrofitt","ERROR")
                // call을 통해서 왜 실패를 했는지 확인을 하고 실패의 이유를 찾음
//                call.isCanceled
//                call.isExecuted
//                call.cancel()
            }

            override fun onResponse( // 통신이 성공적일 때
                call: Call<ArrayList<PersonFromServer>>,
                response: Response<ArrayList<PersonFromServer>>
            ) {
                if(response.isSuccessful) { // 통신시 받은 status code가 정상적으로 넘어왔을 때
                    val personList = response.body() // 서버에 있는 내용을 받아옴 앞서 Network의 경우 복잡한 코드로 처리해야하지만 라이브러리로 간단하게 해결함
                    // status code가 그대로 넘어옴
                    val code = response.code()

                    val error = response.errorBody() // status code에서 제대로 넘겨받았는지에 대해서 확인을 함
                    val header = response.headers() // 인증 정보 요약본을 보냄
                }
            }

        })
    }
}
```
```kotlin
package techtown.org.fastcampus

import retrofit2.Call
import retrofit2.http.GET
// Retrofit에서 주소관리
interface RetrofitService { // interface를 통해서 Url을 관리함, Retrofit이 interface로 쓰게끔 설정한 것임
    // @ annotation
    // 아래 주소의 GET 요청을 하는데 그 response가 ArrayList의 타입임
    // 만일 주소가 여러개면 아래에 annotiation이 무수히 많을 것임
    @GET("json/students/") // baseUrl을 설정했으므로 그 뒷부분을 적어두면 됨
    fun getStudentsList(): Call<ArrayList<PersonFromServer>> // Network에서 데이터를 리턴하는 형태처럼 데이터를 받기 위한 함수 받은 객체 데이터를 ArrayList로 받음

}
```

- POST 요청으로 데이터를 보내는 방식
```kotlin
package techtown.org.fastcampus

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.util.Log
import retrofit2.Call
import retrofit2.Callback
import retrofit2.Response
import retrofit2.Retrofit
import retrofit2.converter.gson.GsonConverterFactory

class RetrofitActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_retrofit)

        val retrofit = Retrofit.Builder()
            .baseUrl("http://mellowcode.org/")
            .addConverterFactory(GsonConverterFactory.create())
            .build()

        val service = retrofit.create(RetrofitService::class.java)

        // GET 요청
        service.getStudentsList().enqueue(object : Callback<ArrayList<PersonFromServer>>{
            override fun onFailure(call: Call<ArrayList<PersonFromServer>>, t: Throwable) {
                Log.d("retrofitt","ERROR")
            }

            override fun onResponse(
                call: Call<ArrayList<PersonFromServer>>,
                response: Response<ArrayList<PersonFromServer>>
            ) {
                if(response.isSuccessful) {
                    val personList = response.body()
                    val code = response.code()

                    val error = response.errorBody()
                    val header = response.headers()
                }
            }

        })

        // POST 요청
        val params = HashMap<String, Any>() // POST를 하기 위해서 HashMap을 미리 만듬
        params.put("name","김아무개")
        params.put("age",20)
        params.put("intro","안녕하세요")
        service.createStudent(params).enqueue(object : Callback<PersonFromServer>{ // POST할 데이터를 params로 넘기고 enqueue 처리를 함
            override fun onFailure(call: Call<PersonFromServer>, t: Throwable) {

            }

            override fun onResponse(
                call: Call<PersonFromServer>,
                response: Response<PersonFromServer>
            ) {
                if (response.isSuccessful) {
                    val person = response.body()
                }
            }
        })
    }
}
```
```kotlin
package techtown.org.fastcampus

import retrofit2.Call
import retrofit2.http.Body
import retrofit2.http.GET
import retrofit2.http.POST

interface RetrofitService {

    @GET("json/students/")
    fun getStudentsList(): Call<ArrayList<PersonFromServer>>

    @POST("json/students/") // 정보를 보내기 위한 요소
    fun createStudent(
        @Body params : HashMap<String, Any> // key-value 방식으로 데이터를 넘겨주므로 이를 해쉬맵을 사용해서 함
    ): Call<PersonFromServer> // 이러한 리턴 타입이 올거라고 정해둠

}
```

- 위와 같이 일일이 다 HashMap 처리를 하지 않고 다른 방법으로 할 수 있음
```kotlin
package techtown.org.fastcampus

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.util.Log
import retrofit2.Call
import retrofit2.Callback
import retrofit2.Response
import retrofit2.Retrofit
import retrofit2.converter.gson.GsonConverterFactory

class RetrofitActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_retrofit)

        val retrofit = Retrofit.Builder()
            .baseUrl("http://mellowcode.org/")
            .addConverterFactory(GsonConverterFactory.create())
            .build()

        val service = retrofit.create(RetrofitService::class.java)

        // GET 요청
        service.getStudentsList().enqueue(object : Callback<ArrayList<PersonFromServer>>{
            override fun onFailure(call: Call<ArrayList<PersonFromServer>>, t: Throwable) {
                Log.d("retrofitt","ERROR")
            }

            override fun onResponse(
                call: Call<ArrayList<PersonFromServer>>,
                response: Response<ArrayList<PersonFromServer>>
            ) {
                if(response.isSuccessful) {
                    val personList = response.body()
                    val code = response.code()

                    val error = response.errorBody()
                    val header = response.headers()
                }
            }

        })

        // POST 요청 (1)
//        val params = HashMap<String, Any>() // POST를 하기 위해서 HashMap을 미리 만듬
//        params.put("name","김아무개")
//        params.put("age",20)
//        params.put("intro","안녕하세요")
//        service.createStudent(params).enqueue(object : Callback<PersonFromServer>{ // POST할 데이터를 params로 넘기고 enqueue 처리를 함
//            override fun onFailure(call: Call<PersonFromServer>, t: Throwable) {
//
//            }
//
//            override fun onResponse(
//                call: Call<PersonFromServer>,
//                response: Response<PersonFromServer>
//            ) {
//                if (response.isSuccessful) {
//                    val person = response.body()
//                }
//            }
//        })

        // POST 요청 (2)
        // 객체를 그대로 넘기는 처리
        val person = PersonFromServer(name = "김철수",age = 12, intro = "안녕하세요 철수입니다") // id는 서버에서 유저를 판단하기 위한 고유값이기 때문에 넣어줄 필요없음
        service.createStudentEasy(person).enqueue(object : Callback<PersonFromServer>{ // POST할 데이터를 params로 넘기고 enqueue 처리를 함
            override fun onFailure(call: Call<PersonFromServer>, t: Throwable) {

            }

            override fun onResponse(
                call: Call<PersonFromServer>,
                response: Response<PersonFromServer>
            ) {
                if (response.isSuccessful) {
                    val person = response.body()
                }
            }
        })
    }
}
```
```kotlin
package techtown.org.fastcampus

import retrofit2.Call
import retrofit2.http.Body
import retrofit2.http.GET
import retrofit2.http.POST

interface RetrofitService {

    @GET("json/students/")
    fun getStudentsList(): Call<ArrayList<PersonFromServer>>

    @POST("json/students/") // 정보를 보내기 위한 요소
    fun createStudent(
        @Body params : HashMap<String, Any> // key-value 방식으로 데이터를 넘겨주므로 이를 해쉬맵을 사용해서 함
    ): Call<PersonFromServer> // 이러한 리턴 타입이 올거라고 정해둠

    @POST("json/students/")
    fun createStudentEasy( // HashMap이 아닌 객체를 이용해서 데이터를 넘기는 것
        @Body person : PersonFromServer
    ): Call<PersonFromServer>

}
```