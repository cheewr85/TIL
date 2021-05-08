## Recyclerview
- 장점
    - ListView의 개선판
        - ViewHolder 포함

    - 유연하다
        - LayoutManager
            - Linear (수직, 수평)
            - Grid (바둑판 형태)
            - StaggeredGrid (생김새가 불규칙한 바둑판 형태)

- 실습
```Kotlin
package techtown.org.fastcampus

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import android.widget.TextView
import androidx.recyclerview.widget.LinearLayoutManager
import androidx.recyclerview.widget.RecyclerView
import kotlinx.android.synthetic.main.activity_recycler_view.*

class RecyclerViewActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_recycler_view)

        val carList = ArrayList<CarForList>()
        for(i in 0 until 10){
            carList.add(CarForList(""+i+"번째 자동차",""+i+"순위 엔진"))
        }

        val adapter = RecylcerViewAdapter(carList, LayoutInflater.from(this@RecyclerViewActivity)) // adapter를 만듬
        recycler_view.adapter = adapter // 어댑터를 리사이클러뷰에 넣어줌
        recycler_view.layoutManager = LinearLayoutManager(this@RecyclerViewActivity) // 레이아웃 매니저로 유연하게 활용할 수 있음
    }
}

class RecylcerViewAdapter(
        val itemList : ArrayList<CarForList>,
        val inflater : LayoutInflater
): RecyclerView.Adapter<RecylcerViewAdapter.ViewHolder>(){ // Adapter를 상속 받음 ViewHolder를 받아야함, 이너 클래스로 만든것을 복붙해서 써도 됨, 타입은 Adapter의 타입으로

    // ViewHolder를 이너 클래스로 만들고 리사이클러뷰 뷰홀더 상속받음
    class ViewHolder(itemView : View):RecyclerView.ViewHolder(itemView){ // 생성자에서 받은 itemView를 넘겨줌
        val carName: TextView
        val carEngine: TextView

        init{ // 어댑터가 생성되자마자 carName, Engine을 생성할 것임
            carName = itemView.findViewById(R.id.car_name)
            carEngine = itemView.findViewById(R.id.car_engine)

        }
    }

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ViewHolder { // ViewHolder를 바탕으로 그려주는 것
        val view = inflater.inflate(R.layout.item_view, parent, false) // 아이템이 들어갈 뷰를 만들어줌
        return ViewHolder(view) // 위의 viewHolder에 그 만든 뷰를 리턴해서 줌, 그러면 ViewHolder에서 init을 통해서 해당 TextView를 만들고 아래 onBindViewHolder를 통해서 데이터가 들어감
    }

    override fun getItemCount(): Int { // 개수를 체크하는 것
        return itemList.size
    }

    override fun onBindViewHolder(holder: ViewHolder, position: Int) { // 가지고 있는 viewHolder에서 View들을 묶어주는 것
        // holder는 위에서 만든 ViewHolder를 사용하는 것임
        holder.carName.setText(itemList.get(position).name)
        holder.carEngine.setText(itemList.get(position).engine)
    }
}
```
- 실습
```Kotlin
package techtown.org.fastcampus

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.util.Log
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import android.widget.TextView
import androidx.recyclerview.widget.GridLayoutManager
import androidx.recyclerview.widget.LinearLayoutManager
import androidx.recyclerview.widget.RecyclerView
import kotlinx.android.synthetic.main.activity_recycler_view.*

class RecyclerViewActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_recycler_view)

        val carList = ArrayList<CarForList>()
        for(i in 0 until 10){
            carList.add(CarForList(""+i+"번째 자동차",""+i+"순위 엔진"))
        }

        val adapter = RecylcerViewAdapter(carList, LayoutInflater.from(this@RecyclerViewActivity)) // adapter를 만듬
        recycler_view.adapter = adapter // 어댑터를 리사이클러뷰에 넣어줌
        recycler_view.layoutManager = LinearLayoutManager(this@RecyclerViewActivity) // 레이아웃 매니저로 유연하게 활용할 수 있음
//        recycler_view.layoutManager = GridLayoutManager(this@RecyclerViewActivity, 2) // 두 줄씩 나오게 함

    }
}

class RecylcerViewAdapter(
        val itemList : ArrayList<CarForList>,
        val inflater : LayoutInflater
): RecyclerView.Adapter<RecylcerViewAdapter.ViewHolder>(){ // Adapter를 상속 받음 ViewHolder를 받아야함, 이너 클래스로 만든것을 복붙해서 써도 됨, 타입은 Adapter의 타입으로

    // ViewHolder를 이너 클래스로 만들고 리사이클러뷰 뷰홀더 상속받음
    inner class ViewHolder(itemView : View):RecyclerView.ViewHolder(itemView){ // 생성자에서 받은 itemView를 넘겨줌, inner를 쓰지 않으면 init에 itemList에 접근을 할 수 없음
        // inner를 쓰면 ViewHolder는 RecyclerViewAdapter에 속하게 됨
        val carName: TextView
        val carEngine: TextView

        init{ // 어댑터가 생성되자마자 carName, Engine을 생성할 것임
            carName = itemView.findViewById(R.id.car_name)
            carEngine = itemView.findViewById(R.id.car_engine)
            itemView.setOnClickListener { // ViewHolder에 View들이 들어오기 때문에 onClickListener를 달음
                val position: Int = adapterPosition // position을 Int로 몇 번째인지 돌려줌
                val engineName = itemList.get(position).engine
                Log.d("engine",engineName)
            }

        }
    }

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ViewHolder { // ViewHolder를 바탕으로 그려주는 것
        val view = inflater.inflate(R.layout.item_view, parent, false) // 아이템이 들어갈 뷰를 만들어줌
        return ViewHolder(view) // 위의 viewHolder에 그 만든 뷰를 리턴해서 줌, 그러면 ViewHolder에서 init을 통해서 해당 TextView를 만들고 아래 onBindViewHolder를 통해서 데이터가 들어감
    }

    override fun getItemCount(): Int { // 개수를 체크하는 것
        return itemList.size
    }

    override fun onBindViewHolder(holder: ViewHolder, position: Int) { // 가지고 있는 viewHolder에서 View들을 묶어주는 것
        // holder는 위에서 만든 ViewHolder를 사용하는 것임
        holder.carName.setText(itemList.get(position).name)
        holder.carEngine.setText(itemList.get(position).engine)
    }
}
```