## Addview
- 리스트뷰 
	- 유사하게 반복되는 뷰를 그리기 위한 도구

- 리스트뷰를 그리는 방법
	- addView
		- 실제로 리스트뷰를 그리기 위해서 잘 사용되지 않는다
		- Item을 담을 xml을 만들어준다
		- 그 xml에 내용을 채워준다
		- Container View에 더해준다
		- 반복한다
	- ListView -> 예전에 많이 사용되었다
	- RecyclerView -> 최근에 가장 많이 사용이 되고 있고 가장 효율이 높다

- 실습
```Kotlin
package techtown.org.fastcampus

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.view.LayoutInflater
import android.widget.LinearLayout
import android.widget.TextView

class AddViewActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_add_view)


        // 아이템 리스트 준비, 만일 아이템이 오버하면 스크롤 뷰를 활용해서 스크롤 할 수 있게끔 해야함
        val carList = ArrayList<CarForList>()
        for(i in 0 until 10){
            carList.add(CarForList(""+i+"번째 자동차",""+i+"순위 엔진"))
        }

        val container = findViewById<LinearLayout>(R.id.addview_container)
        val inflater = LayoutInflater.from(this@AddViewActivity)
        for(i in 0 until carList.size){
            val itemView = inflater.inflate(R.layout.item_view,null)
            val carNameView = itemView.findViewById<TextView>(R.id.car_name)
            val carEngineView = itemView.findViewById<TextView>(R.id.car_engine)

            carNameView.setText(carList.get(i).name)
            carEngineView.setText(carList.get(i).engine)
            container.addView(itemView)
        }
    }



}

class CarForList(val name : String, val engine : String) {

}
```

![one](/img/Android/android/Addview/one.png)