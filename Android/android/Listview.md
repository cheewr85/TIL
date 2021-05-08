## Listview
1. 리스트로 만들고 싶은 아이템의 리스트를 준비한다
2. 인플레이터를 준비한다
3. 인플레이터로 아이템 하나에 해당하는 뷰를 만들어 준다
4. 위에서 만든 뷰를 컨테이너 뷰에 붙여준다

ListView
1. 리스트를 만들고 싶은 아이템의 리스트를 준비한다
2. Adapter를 이용한다

AddView와 ListView의 차이점
1. 만드는 방식이 다르다
2. 그리는 방식이 다르다
    - AddView -> 리스트의 갯수와 상관없이 한 번에 다 그림
    - ListView -> 보여지는 부분 + a만 한번에 그리고 필요한 경우에 더 그린다

- 실습
```Kotlin
package techtown.org.fastcampus

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import android.widget.BaseAdapter
import android.widget.TextView
import kotlinx.android.synthetic.main.activity_list_view.*

class ListViewActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_list_view)

        val carList = ArrayList<CarForList>()
        for(i in 0 until 10){
            carList.add(CarForList(""+i+"번째 자동차",""+i+"순위 엔진"))
        }
        val adapter = ListViewAdapter(carList, LayoutInflater.from(this@ListViewActivity)) // adapter를 통해서 연결해줌
        listView.adapter = adapter
    }
}


class ListViewAdapter(val carForList : ArrayList<CarForList>, val layoutInflater : LayoutInflater) : BaseAdapter() { // 생성자 만듬


    override fun getView(position: Int, convertView: View?, parent: ViewGroup?): View { // 뷰를 그려주는 것
        val view = layoutInflater.inflate(R.layout.item_view,null)
        var carNameTextview = view.findViewById<TextView>(R.id.car_name)
        var carEngineTextview = view.findViewById<TextView>(R.id.car_engine)

        carNameTextview.setText(carForList.get(position).name)
        carEngineTextview.setText(carForList.get(position).engine)

        return view
    }

    override fun getItem(position: Int): Any { // Listview의 순서를 의미함 해당 인덱스 아이템정보 알려줌, 0,1,2,3,4의 순서 몇번째인지를 리턴함
        // 그리고자 하는 아이템 리스트의 하나(포지션에 해당하는)
        return carForList.get(position)
    }

    override fun getItemId(position: Int): Long { // ListView의 각각 아이템 번째의 아이디를 부여해줌
        // 해당 포지션에 위치해 있는 아이템 뷰의 아이디 설정
        return position.toLong()
    }

    override fun getCount(): Int { // 몇 개가 있는지 알려준 것
        // 그리고자 하는 아이템 리스트의 전체 개수
        return carForList.size // 몇 개를 보여줘야 하는지 알아야하기 때문에 전체 개수를 return 함
    }

}
```

- addview와 상당히 유사한 구조를 가짐

![one](/img/Android/android/Listview/one.png)

- listview에 리스너를 장착, 각각의 Item클릭시 이벤트 발생, 리스트뷰의 속성을 검색해서 활용할수도 있음 xml 파일에서

```Kotlin
package techtown.org.fastcampus

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import android.widget.BaseAdapter
import android.widget.TextView
import android.widget.Toast
import kotlinx.android.synthetic.main.activity_list_view.*

class ListViewActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_list_view)

        val carList = ArrayList<CarForList>()
        for(i in 0 until 10){
            carList.add(CarForList(""+i+"번째 자동차",""+i+"순위 엔진"))
        }
        val adapter = ListViewAdapter(carList, LayoutInflater.from(this@ListViewActivity)) // adapter를 통해서 연결해줌
        listView.adapter = adapter
        listView.setOnItemClickListener { parent, view, position, id -> // 아이템 클릭시 토스트 메시지 발생
            val carName = (adapter.getItem(position) as CarForList).name // 아이템을 리턴받고 CarForList로 캐스팅 후 이름과 엔진을 받음
            val carEngine = (adapter.getItem(position) as CarForList).engine

            Toast.makeText(this@ListViewActivity, carName + " " + carEngine, Toast.LENGTH_SHORT).show() // 토스트 메시지 생성
        }
    }
}


class ListViewAdapter(val carForList : ArrayList<CarForList>, val layoutInflater : LayoutInflater) : BaseAdapter() { // 생성자 만듬


    override fun getView(position: Int, convertView: View?, parent: ViewGroup?): View { // 뷰를 그려주는 것
        val view = layoutInflater.inflate(R.layout.item_view,null)
        var carNameTextview = view.findViewById<TextView>(R.id.car_name)
        var carEngineTextview = view.findViewById<TextView>(R.id.car_engine)

        carNameTextview.setText(carForList.get(position).name)
        carEngineTextview.setText(carForList.get(position).engine)

        return view
    }

    override fun getItem(position: Int): Any { // Listview의 순서를 의미함 해당 인덱스 아이템정보 알려줌, 0,1,2,3,4의 순서 몇번째인지를 리턴함
        // 그리고자 하는 아이템 리스트의 하나(포지션에 해당하는)
        return carForList.get(position)
    }

    override fun getItemId(position: Int): Long { // ListView의 각각 아이템 번째의 아이디를 부여해줌
        // 해당 포지션에 위치해 있는 아이템 뷰의 아이디 설정
        return position.toLong()
    }

    override fun getCount(): Int { // 몇 개가 있는지 알려준 것
        // 그리고자 하는 아이템 리스트의 전체 개수
        return carForList.size // 몇 개를 보여줘야 하는지 알아야하기 때문에 전체 개수를 return 함
    }

}
```

- findViewById를 활용하는 것이 무겁고 개선의 여지가 있으므로 위의 코드를 ViewHolder를 사용할 것임, Holder에다가 쓸 View를 담아두고 돌려서 쓸 것임

```Kotlin
package techtown.org.fastcampus

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import android.widget.BaseAdapter
import android.widget.TextView
import android.widget.Toast
import kotlinx.android.synthetic.main.activity_list_view.*

class ListViewActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_list_view)

        val carList = ArrayList<CarForList>()
        for(i in 0 until 10){
            carList.add(CarForList(""+i+"번째 자동차",""+i+"순위 엔진"))
        }
        val adapter = ListViewAdapter(carList, LayoutInflater.from(this@ListViewActivity)) // adapter를 통해서 연결해줌
        listView.adapter = adapter
        listView.setOnItemClickListener { parent, view, position, id -> // 아이템 클릭시 토스트 메시지 발생
            val carName = (adapter.getItem(position) as CarForList).name // 아이템을 리턴받고 CarForList로 캐스팅 후 이름과 엔진을 받음
            val carEngine = (adapter.getItem(position) as CarForList).engine

            Toast.makeText(this@ListViewActivity, carName + " " + carEngine, Toast.LENGTH_SHORT).show() // 토스트 메시지 생성
        }
    }
}


class ListViewAdapter(val carForList : ArrayList<CarForList>, val layoutInflater : LayoutInflater) : BaseAdapter() { // 생성자 만듬


    override fun getView(position: Int, convertView: View?, parent: ViewGroup?): View { // 뷰를 그려주는 것, convertView는 도는 것을 의미 재활용 하는 것

        val view : View
        val holder : ViewHolder

        if (convertView == null) { // 재사용할 것이 없으면 inflater를 하는 것, 첫 시작은 화면에 보이기 때문에 바로 만들어야 하지만 그 이후는 계속 거의 재사용을 함
            view = layoutInflater.inflate(R.layout.item_view,null)
            holder = ViewHolder()

            // view를 찾은 뒤 holder에 집어 넣는 것임
            holder.carName = view.findViewById(R.id.car_name)
            holder.carEngine = view.findViewById(R.id.car_engine)

            view.tag = holder // 찾을 수 있게 태그를 달음
        } else { // 만일 재사용할 것이 있다면 태그를 통해서 ViewHolder로 바꾼 후 다시 내용을 채워줌
            holder = convertView.tag as ViewHolder
            view = convertView
        }
        // null이 가능하므로 null이 아닌 경우에 할당하게끔 처리를 하게함
        holder.carName?.setText(carForList.get(position).name)
        holder.carEngine?.setText(carForList.get(position).engine)

        return view
    }

    override fun getItem(position: Int): Any { // Listview의 순서를 의미함 해당 인덱스 아이템정보 알려줌, 0,1,2,3,4의 순서 몇번째인지를 리턴함
        // 그리고자 하는 아이템 리스트의 하나(포지션에 해당하는)
        return carForList.get(position)
    }

    override fun getItemId(position: Int): Long { // ListView의 각각 아이템 번째의 아이디를 부여해줌
        // 해당 포지션에 위치해 있는 아이템 뷰의 아이디 설정
        return position.toLong()
    }

    override fun getCount(): Int { // 몇 개가 있는지 알려준 것
        // 그리고자 하는 아이템 리스트의 전체 개수
        return carForList.size // 몇 개를 보여줘야 하는지 알아야하기 때문에 전체 개수를 return 함
    }

}

class ViewHolder {
    var carName: TextView? = null
    var carEngine: TextView? = null
}
```