## Tablayout, Pager
- Pager
	- 종이 넘기듯이 화면을 넘겨주는 역할
- TabLayout
	- tab을 담당하는 역할
- Adapter
	- Tablayout과 Pager를 연결해주는 역할

### 실습
- 탭을 만들고 Pager를 활용하고 프래그먼트를 통해서 만듬
```kotlin
package techtown.org.fastcampus

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import androidx.fragment.app.Fragment
import androidx.fragment.app.FragmentManager
import androidx.fragment.app.FragmentStatePagerAdapter
import kotlinx.android.synthetic.main.activity_tab_pager.*

class TabPagerActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_tab_pager)

        // tablayout과 pager를 연결하기 위해서 리스너를 씀
        tab_layout.addTab(tab_layout.newTab().setText("ONE")) // 새로운 탭을 만들어서 ONE이라는 이름을 지어서 만듬
        tab_layout.addTab(tab_layout.newTab().setText("TWO"))
        tab_layout.addTab(tab_layout.newTab().setText("THREE"))
    }
}

// pager에서 화면을 여러개 붙이기 위해서 Adapter를 달음, ListViwe와 유사하게
// pager를 통해서 스와이프 하면서 화면을 볼 수 있음

class PagerAdapter(
        fragmentManager: FragmentManager, // 프래그먼트를 활용할 것임, 리스트가 프래그먼트로 구성되어 있음
        val tabCount : Int
): FragmentStatePagerAdapter(fragmentManager) {
    override fun getItem(position: Int): Fragment { // 아이템 하나를 찾을 때 해당 함수를 통해서 얻음
        // position에 해당하는 Fragment를 리턴해 줘야함
        when(position) { // 각각의 Fragment를 연결해줌
            0 -> {
                return Fragment1()
            }
            1 -> {
                return Fragment2()
            }
            2 -> {
                return Fragment3()
            }
            else -> return Fragment1()
        }
    }

    override fun getCount(): Int { // 전체 사이즈 리턴
        return tabCount
    }

}
```

- 실습2 페이저와 탭레이아웃 연결
```kotlin
package techtown.org.fastcampus

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import androidx.fragment.app.Fragment
import androidx.fragment.app.FragmentManager
import androidx.fragment.app.FragmentStatePagerAdapter
import com.google.android.material.tabs.TabLayout
import kotlinx.android.synthetic.main.activity_tab_pager.*

class TabPagerActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_tab_pager)

        // tablayout과 pager를 연결하기 위해서 리스너를 씀
        tab_layout.addTab(tab_layout.newTab().setText("ONE")) // 새로운 탭을 만들어서 ONE이라는 이름을 지어서 만듬
        tab_layout.addTab(tab_layout.newTab().setText("TWO"))
        tab_layout.addTab(tab_layout.newTab().setText("THREE"))
        
        // Pager에서 Adapter를 설정함
        val pagerAdapter = PagerAdapter(supportFragmentManager, 3)
        view_pager.adapter = pagerAdapter

        // Pager에 Adapter를 설정해도 탭과 연동이 되지 않음, 그러므로 아래와 같이 리스너를 설정해줘야함
        tab_layout.addOnTabSelectedListener(object: TabLayout.OnTabSelectedListener {
            override fun onTabReselected(tab: TabLayout.Tab?) {

            }

            override fun onTabUnselected(tab: TabLayout.Tab?) {

            }

            override fun onTabSelected(tab: TabLayout.Tab?) { // 탭이 클릭 됐을 때
                view_pager.currentItem = tab!!.position // viewpager에서 현재 Item을 tab에서의 포지션에 연결시킴, pager가 움직이면 tab도 움직일 수 있게끔
            }
        })
        view_pager.addOnPageChangeListener(TabLayout.TabLayoutOnPageChangeListener(tab_layout)) // -> pager가 이동했을 때 탭을 이동시키는 코드임
   }
}

// pager에서 화면을 여러개 붙이기 위해서 Adapter를 달음, ListViwe와 유사하게
// pager를 통해서 스와이프 하면서 화면을 볼 수 있음

class PagerAdapter(
        fragmentManager: FragmentManager, // 프래그먼트를 활용할 것임, 리스트가 프래그먼트로 구성되어 있음
        val tabCount : Int
): FragmentStatePagerAdapter(fragmentManager) {
    override fun getItem(position: Int): Fragment { // 아이템 하나를 찾을 때 해당 함수를 통해서 얻음
        // position에 해당하는 Fragment를 리턴해 줘야함
        when(position) { // 각각의 Fragment를 연결해줌
            0 -> {
                return Fragment1()
            }
            1 -> {
                return Fragment2()
            }
            2 -> {
                return Fragment3()
            }
            else -> return Fragment1()
        }
    }

    override fun getCount(): Int { // 전체 사이즈 리턴
        return tabCount
    }

}
```

- 실습3 → 위처럼 Fragment를 각각 만들어서 return 해주면 무거워짐
- 아래와 같이 레이아웃 Inflater를 활용하여 view를 그려줌으로써 각각의 Fragment를 쓰는 것을 간소화 함 그린 xml을 활용함
```kotlin
package techtown.org.fastcampus

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import androidx.viewpager.widget.PagerAdapter
import com.google.android.material.tabs.TabLayout
import kotlinx.android.synthetic.main.activity_tab_pager.*

class TabPager2Activity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_tab_pager)

        // 동일하게 탭과 adapter를 처리해줌
        tab_layout.addTab(tab_layout.newTab().setText("ONE"))
        tab_layout.addTab(tab_layout.newTab().setText("TWO"))
        tab_layout.addTab(tab_layout.newTab().setText("THREE"))

        val adapter = ThreePageAdapter(LayoutInflater.from(this@TabPager2Activity))
        view_pager.adapter = adapter
        view_pager.addOnPageChangeListener(TabLayout.TabLayoutOnPageChangeListener(tab_layout))

        tab_layout.addOnTabSelectedListener(object: TabLayout.OnTabSelectedListener {
            override fun onTabReselected(tab: TabLayout.Tab?) {

            }

            override fun onTabUnselected(tab: TabLayout.Tab?) {

            }

            override fun onTabSelected(tab: TabLayout.Tab?) {
                view_pager.currentItem = tab!!.position
            }
        })
        view_pager.addOnPageChangeListener(TabLayout.TabLayoutOnPageChangeListener(tab_layout))

    }
}

class ThreePageAdapter(
    val layoutInflater: LayoutInflater
) : PagerAdapter(){
    
    override fun instantiateItem(container: ViewGroup, position: Int): Any { // 뷰를 그려줌
        when(position){
            0->{
                val view = layoutInflater.inflate(R.layout.fragment_one,container,false)
                container.addView(view)
                return view
            }
            1->{
                val view = layoutInflater.inflate(R.layout.fragment_two,container,false)
                container.addView(view)
                return view
            }
            2->{
                val view = layoutInflater.inflate(R.layout.fragment_three,container,false)
                container.addView(view)
                return view
            }
            else->{
                val view = layoutInflater.inflate(R.layout.fragment_one,container,false)
                container.addView(view)
                return view
            }

        }
    }

    override fun destroyItem(container: ViewGroup, position: Int, `object`: Any) { // 페이저를 넘겨서 뷰가 사라질 때 Item을 없앰
        container.removeView(`object` as View) // item을 없애는 것이므로 container에서 view를 떼냄
    }

    override fun getCount(): Int { // Pager의 카운트를 넣으면 됨
        return 3
    }

    override fun isViewFromObject(view: View, `object`: Any): Boolean { // Viewpager에서 화면에 나온 것이 작성자가 만든것이 맞는지 확인하는 것
        return view === `object` as View // view와 object가 갖는지 확인 boolean으로 리턴함 , === 는 좀 더 정확한 비교임, 즉 단순값 비교가 아닌 주소값까지 비교함, 아예 주소값까지 같은지 확인을 함
        // 위에서 instantiateItem을 통해서 받은 view가 처리하기 위한 object에서의 view와 같은지를 비교하는 것임
        // ` 표시는 자바에서 object는 별 뜻이 없지만 코틀린에서는 그렇지 않으므로 코틀린에서 `를 활용해서 구분함
    }
}
```